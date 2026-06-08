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

const VERT_COUNT  = 24
const HORIZ_COUNT = 28
const GRID_WIDTH  = 30
const GRID_DEPTH  = 30
const SPEED       = 5.5
const Y_PLANE     = -1.5

const horizZ: number[] = []

function lerp(a: number, b: number, t: number) { return a + (b - a) * t }

function makeVertLines(): THREE.LineSegments {
  const pos: number[] = []
  const col: number[] = []
  for (let i = 0; i < VERT_COUNT; i++) {
    const t = i / (VERT_COUNT - 1)
    const x = (t - 0.5) * GRID_WIDTH
    pos.push(x, Y_PLANE, 0,   x, Y_PLANE, -GRID_DEPTH)
    // near: yellow, far: dark
    col.push(1, 0.89, 0,  0.06, 0.055, 0)
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

    // brightness by depth
    const t = Math.max(0, (z + GRID_DEPTH) / GRID_DEPTH)
    const r = lerp(0.06, 1,    t)
    const g = lerp(0.05, 0.89, t)
    ca[idx]=r; ca[idx+1]=g; ca[idx+2]=0
    ca[idx+3]=r; ca[idx+4]=g; ca[idx+5]=0
  }
  posAttr.needsUpdate = true
  colAttr.needsUpdate = true
}

function onMouseMove(e: MouseEvent) {
  mouse.x = (e.clientX / window.innerWidth  - 0.5) * 2
  mouse.y = (e.clientY / window.innerHeight - 0.5) * 2
}

function onResize() {
  const c = canvasRef.value
  if (!c || !renderer || !camera) return
  renderer.setSize(c.clientWidth, c.clientHeight, false)
  camera.aspect = c.clientWidth / c.clientHeight
  camera.updateProjectionMatrix()
}

onMounted(() => {
  const c = canvasRef.value!
  scene    = new THREE.Scene()
  camera   = new THREE.PerspectiveCamera(70, c.clientWidth / c.clientHeight, 0.1, 200)
  camera.position.set(0, 3, 6)
  camera.lookAt(0, Y_PLANE, -GRID_DEPTH * 0.5)

  renderer = new THREE.WebGLRenderer({ canvas: c, antialias: true, alpha: true })
  renderer.setSize(c.clientWidth, c.clientHeight, false)
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  renderer.setClearColor(0x000000, 0)

  // Horizon glow plane (flat large quad with emissive material)
  const sunGeo  = new THREE.CircleGeometry(3.5, 64)
  const sunMat  = new THREE.MeshBasicMaterial({ color: 0xffe500, transparent: true, opacity: 0.12 })
  const sun     = new THREE.Mesh(sunGeo, sunMat)
  sun.position.set(0, Y_PLANE + 0.01, -GRID_DEPTH + 2)
  sun.rotation.x = -Math.PI / 2
  scene.add(sun)

  // Horizon line
  const hlGeo = new THREE.BufferGeometry()
  hlGeo.setAttribute('position', new THREE.BufferAttribute(
    new Float32Array([-GRID_WIDTH/2, Y_PLANE, -GRID_DEPTH+1, GRID_WIDTH/2, Y_PLANE, -GRID_DEPTH+1]), 3
  ))
  const hl = new THREE.LineSegments(hlGeo, new THREE.LineBasicMaterial({ color: 0xffe500 }))
  scene.add(hl)

  scene.add(makeVertLines())
  scene.add(makeHorizLines())

  window.addEventListener('mousemove', onMouseMove)
  window.addEventListener('resize', onResize)

  function animate(ts: number) {
    rafId = requestAnimationFrame(animate)
    const dt = Math.min((ts - lastTime) / 1000, 0.05)
    lastTime = ts

    updateHoriz(dt)

    // subtle camera sway on mouse
    camera.position.x += (mouse.x * 1.5 - camera.position.x) * 0.04
    camera.lookAt(0, Y_PLANE, -GRID_DEPTH * 0.5)

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
}
</style>
