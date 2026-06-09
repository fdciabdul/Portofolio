<script setup lang="ts">
import { onMounted, onBeforeUnmount, ref } from 'vue'
import * as THREE from 'three'

const canvasRef = ref<HTMLCanvasElement | null>(null)

let renderer: THREE.WebGLRenderer
let scene: THREE.Scene
let camera: THREE.PerspectiveCamera
let horizGeo: THREE.BufferGeometry
let rafId: number
let lastTime = 0
const mouse = { x: 0, y: 0 }

// chunky-pixel look: render small, upscale with CSS image-rendering: pixelated
const PIXEL_SCALE = 3

const VERT_COUNT  = 24
const HORIZ_COUNT = 28
const GRID_WIDTH  = 30
const GRID_DEPTH  = 30
const SPEED       = 5.5
const Y_PLANE     = -1.5

// 8-bit palette (lime / teal / white / dark)
const PALETTE = [0x9eff00, 0x00e0b8, 0xffffff, 0x1a3a00]

const horizZ: number[] = []

// scrolling voxel buildings
interface Building { mesh: THREE.Mesh }
const buildings: Building[] = []
const BUILDING_ROWS = 11
const Z_NEAR = 4
const Z_STEP = GRID_DEPTH / BUILDING_ROWS

// center rotating voxel cluster
let cluster: THREE.Group

function lerp(a: number, b: number, t: number) { return a + (b - a) * t }

function makeVertLines(): THREE.LineSegments {
  const pos: number[] = []
  const col: number[] = []
  for (let i = 0; i < VERT_COUNT; i++) {
    const t = i / (VERT_COUNT - 1)
    const x = (t - 0.5) * GRID_WIDTH
    pos.push(x, Y_PLANE, 0,   x, Y_PLANE, -GRID_DEPTH)
    col.push(0.62, 1, 0,  0.03, 0.06, 0)
  }
  const geo = new THREE.BufferGeometry()
  geo.setAttribute('position', new THREE.BufferAttribute(new Float32Array(pos), 3))
  geo.setAttribute('color',    new THREE.BufferAttribute(new Float32Array(col), 3))
  return new THREE.LineSegments(geo, new THREE.LineBasicMaterial({ vertexColors: true }))
}

function makeHorizLines(): THREE.LineSegments {
  const pos = new Float32Array(HORIZ_COUNT * 6)
  const col = new Float32Array(HORIZ_COUNT * 6)
  for (let i = 0; i < HORIZ_COUNT; i++) {
    horizZ[i] = -((i / HORIZ_COUNT) * GRID_DEPTH)
  }
  const geo = new THREE.BufferGeometry()
  geo.setAttribute('position', new THREE.BufferAttribute(pos, 3))
  geo.setAttribute('color',    new THREE.BufferAttribute(col, 3))
  horizGeo = geo
  return new THREE.LineSegments(geo, new THREE.LineBasicMaterial({ vertexColors: true }))
}

function updateHoriz(dt: number) {
  const posAttr = horizGeo.attributes.position
  const colAttr = horizGeo.attributes.color
  if (!posAttr || !colAttr) return
  const pa = posAttr.array as Float32Array
  const ca = colAttr.array as Float32Array
  const hw = GRID_WIDTH / 2

  for (let i = 0; i < HORIZ_COUNT; i++) {
    let z = (horizZ[i] ?? 0) + SPEED * dt
    if (z > 0.5) z -= GRID_DEPTH
    horizZ[i] = z

    const idx = i * 6
    pa[idx]     = -hw; pa[idx+1] = Y_PLANE; pa[idx+2] = z
    pa[idx+3]   =  hw; pa[idx+4] = Y_PLANE; pa[idx+5] = z

    const t = Math.max(0, (z + GRID_DEPTH) / GRID_DEPTH)
    const r = lerp(0.03, 0.62, t)
    const g = lerp(0.06, 1,    t)
    ca[idx]=r; ca[idx+1]=g; ca[idx+2]=0
    ca[idx+3]=r; ca[idx+4]=g; ca[idx+5]=0
  }
  posAttr.needsUpdate = true
  colAttr.needsUpdate = true
}

// build one voxel "building" — a box with a lime wireframe outline
function makeBuilding(side: number, row: number): Building {
  const h = 0.8 + ((row * 7 + side * 13) % 5) * 0.9          // pseudo-random height
  const w = 1.4
  const color = PALETTE[(row + (side > 0 ? 1 : 0)) % 2 === 0 ? 3 : 1]!  // dark or teal body
  const geo = new THREE.BoxGeometry(w, h, w)
  const mat = new THREE.MeshLambertMaterial({ color })
  const mesh = new THREE.Mesh(geo, mat)

  // lime wireframe edges for the 8-bit pop
  const edges = new THREE.LineSegments(
    new THREE.EdgesGeometry(geo),
    new THREE.LineBasicMaterial({ color: 0x9eff00 })
  )
  mesh.add(edges)

  const x = side * (4 + ((row * 3) % 3) * 1.4)
  const z = Z_NEAR - row * Z_STEP
  mesh.position.set(x, Y_PLANE + h / 2, z)
  mesh.userData.h = h
  return { mesh }
}

function recycleBuilding(b: Building) {
  // send to far, randomize height
  const h = 0.8 + (Math.abs(Math.round(b.mesh.position.x * 31)) % 5) * 0.9
  const geo = b.mesh.geometry as THREE.BoxGeometry
  const params = geo.parameters
  if (params.height !== h) {
    b.mesh.geometry.dispose()
    const ng = new THREE.BoxGeometry(params.width, h, params.depth)
    b.mesh.geometry = ng
    const edges = b.mesh.children[0] as THREE.LineSegments
    edges.geometry.dispose()
    edges.geometry = new THREE.EdgesGeometry(ng)
    b.mesh.userData.h = h
  }
  b.mesh.position.y = Y_PLANE + h / 2
}

function makeCluster(): THREE.Group {
  const g = new THREE.Group()
  const size = 0.55
  const geo = new THREE.BoxGeometry(size, size, size)
  // 3x3x3 voxel cube with gaps — floating logo
  for (let x = -1; x <= 1; x++)
    for (let y = -1; y <= 1; y++)
      for (let z = -1; z <= 1; z++) {
        if ((x + y + z) % 2 !== 0) continue          // checker gaps = 8-bit look
        const color = PALETTE[(Math.abs(x + y * 2 + z * 3)) % PALETTE.length]!
        const m = new THREE.Mesh(geo, new THREE.MeshLambertMaterial({ color }))
        m.position.set(x * size, y * size, z * size)
        m.add(new THREE.LineSegments(
          new THREE.EdgesGeometry(geo),
          new THREE.LineBasicMaterial({ color: 0x9eff00 })
        ))
        g.add(m)
      }
  g.position.set(0, 1.4, -6)
  return g
}

function onMouseMove(e: MouseEvent) {
  mouse.x = (e.clientX / window.innerWidth  - 0.5) * 2
  mouse.y = (e.clientY / window.innerHeight - 0.5) * 2
}

function onResize() {
  const c = canvasRef.value
  if (!c || !renderer || !camera) return
  renderer.setSize(c.clientWidth / PIXEL_SCALE, c.clientHeight / PIXEL_SCALE, false)
  camera.aspect = c.clientWidth / c.clientHeight
  camera.updateProjectionMatrix()
}

onMounted(() => {
  const c = canvasRef.value!
  scene    = new THREE.Scene()
  camera   = new THREE.PerspectiveCamera(70, c.clientWidth / c.clientHeight, 0.1, 200)
  camera.position.set(0, 3, 6)
  camera.lookAt(0, Y_PLANE + 1, -GRID_DEPTH * 0.4)

  renderer = new THREE.WebGLRenderer({ canvas: c, antialias: false, alpha: true })
  // render at low internal res → chunky pixels via CSS upscaling
  renderer.setSize(c.clientWidth / PIXEL_SCALE, c.clientHeight / PIXEL_SCALE, false)
  renderer.setPixelRatio(1)
  renderer.setClearColor(0x000000, 0)

  // lighting for flat-shaded voxel faces
  scene.add(new THREE.AmbientLight(0x335522, 1.1))
  const key = new THREE.DirectionalLight(0xaaff66, 1.4)
  key.position.set(4, 8, 3)
  scene.add(key)
  const rim = new THREE.DirectionalLight(0x00e0b8, 0.6)
  rim.position.set(-5, 2, -4)
  scene.add(rim)

  // horizon glow
  const sun = new THREE.Mesh(
    new THREE.CircleGeometry(3.5, 48),
    new THREE.MeshBasicMaterial({ color: 0x9eff00, transparent: true, opacity: 0.12 })
  )
  sun.position.set(0, Y_PLANE + 0.01, -GRID_DEPTH + 2)
  sun.rotation.x = -Math.PI / 2
  scene.add(sun)

  const hl = new THREE.LineSegments(
    new THREE.BufferGeometry().setAttribute('position', new THREE.BufferAttribute(
      new Float32Array([-GRID_WIDTH/2, Y_PLANE, -GRID_DEPTH+1, GRID_WIDTH/2, Y_PLANE, -GRID_DEPTH+1]), 3)),
    new THREE.LineBasicMaterial({ color: 0x9eff00 })
  )
  scene.add(hl)

  scene.add(makeVertLines())
  scene.add(makeHorizLines())

  // voxel buildings, both sides
  for (let side = -1; side <= 1; side += 2)
    for (let row = 0; row < BUILDING_ROWS; row++) {
      const b = makeBuilding(side, row)
      buildings.push(b)
      scene.add(b.mesh)
    }

  cluster = makeCluster()
  scene.add(cluster)

  window.addEventListener('mousemove', onMouseMove)
  window.addEventListener('resize', onResize)

  function animate(ts: number) {
    rafId = requestAnimationFrame(animate)
    const dt = Math.min((ts - lastTime) / 1000, 0.05)
    lastTime = ts

    updateHoriz(dt)

    // scroll buildings toward camera, recycle past view
    for (const b of buildings) {
      b.mesh.position.z += SPEED * dt
      if (b.mesh.position.z > Z_NEAR + 2) {
        b.mesh.position.z -= GRID_DEPTH + Z_STEP
        recycleBuilding(b)
      }
    }

    // float + spin the center voxel cluster
    cluster.rotation.y += dt * 0.6
    cluster.rotation.x = Math.sin(ts * 0.0006) * 0.15
    cluster.position.y = 1.4 + Math.sin(ts * 0.0015) * 0.25

    // parallax camera
    camera.position.x += (mouse.x * 1.5 - camera.position.x) * 0.04
    camera.position.y += (3 - mouse.y * 0.8 - camera.position.y) * 0.04
    camera.lookAt(0, Y_PLANE + 1, -GRID_DEPTH * 0.4)

    renderer.render(scene, camera)
  }
  requestAnimationFrame(animate)
})

onBeforeUnmount(() => {
  cancelAnimationFrame(rafId)
  window.removeEventListener('mousemove', onMouseMove)
  window.removeEventListener('resize', onResize)
  renderer?.dispose()
})
</script>

<template>
  <canvas ref="canvasRef" class="hero-canvas" />
</template>

<style scoped>
.hero-canvas {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  display: block;
  image-rendering: pixelated;
  image-rendering: crisp-edges;
}
</style>
