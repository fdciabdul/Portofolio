<script setup lang="ts">
import { ref } from 'vue'

const generating = ref(false)

function goHome() {
  window.location.hash = ''
}

async function imgDataUrl(url: string): Promise<string | null> {
  try {
    const res = await fetch(url)
    const blob = await res.blob()
    return await new Promise((resolve) => {
      const fr = new FileReader()
      fr.onload = () => resolve(fr.result as string)
      fr.onerror = () => resolve(null)
      fr.readAsDataURL(blob)
    })
  } catch {
    return null
  }
}

const DARK = '#111111'
const GRAY = '#444444'

function rule() {
  return { canvas: [{ type: 'line', x1: 0, y1: 0, x2: 515, y2: 0, lineWidth: 1, lineColor: DARK }], margin: [0, 6, 0, 8] as [number, number, number, number] }
}
function h2(t: string) {
  return { text: t.toUpperCase(), bold: true, fontSize: 11, color: DARK, characterSpacing: 1, margin: [0, 0, 0, 6] as [number, number, number, number] }
}
function skill(label: string, val: string) {
  return { text: [{ text: label + ': ', bold: true }, { text: val }], margin: [0, 0, 0, 3] as [number, number, number, number] }
}
function job(title: string, meta: string, bullets: string[] = []) {
  const block: any[] = [{
    columns: [
      { text: title, bold: true, fontSize: 11 },
      { text: meta, color: GRAY, fontSize: 9, alignment: 'right' },
    ],
    margin: [0, 0, 0, bullets.length ? 1 : 6],
  }]
  if (bullets.length) {
    block.push({ ul: bullets, margin: [0, 0, 0, 6], fontSize: 10 })
  }
  return { stack: block, unbreakable: true }
}

async function downloadPdf() {
  if (generating.value) return
  generating.value = true
  try {
    const [pmMod, vfsMod, { jakartaVfs }] = await Promise.all([
      import('pdfmake/build/pdfmake'),
      import('pdfmake/build/vfs_fonts'),
      import('../assets/jakartaVfs'),
    ])
    const pdfMake: any = (pmMod as any).default ?? pmMod
    const baseVfs: any = (vfsMod as any).default ?? (vfsMod as any).vfs ?? vfsMod
    const vfsMap: any = { ...baseVfs, ...jakartaVfs }
    if (typeof pdfMake.addVirtualFileSystem === 'function') {
      pdfMake.addVirtualFileSystem(vfsMap)
    } else {
      pdfMake.vfs = vfsMap
    }
    pdfMake.fonts = {
      PlusJakartaSans: {
        normal: 'PlusJakartaSans-Regular.ttf',
        bold: 'PlusJakartaSans-Bold.ttf',
        italics: 'PlusJakartaSans-Italic.ttf',
        bolditalics: 'PlusJakartaSans-BoldItalic.ttf',
      },
      Roboto: {
        normal: 'Roboto-Regular.ttf',
        bold: 'Roboto-Medium.ttf',
        italics: 'Roboto-Italic.ttf',
        bolditalics: 'Roboto-MediumItalic.ttf',
      },
    }

    const photo = await imgDataUrl('/abdul.jpg')

    const header = {
      columns: [
        ...(photo ? [{ width: 'auto', margin: [0, 2, 14, 0] as [number, number, number, number], stack: [{ image: photo, fit: [72, 72] }] }] : []),
        {
          width: '*',
          stack: [
            { text: 'Abdul Muttaqin', bold: true, fontSize: 22 },
            { text: 'Software Engineer · Fullstack Developer', bold: true, fontSize: 11, margin: [0, 2, 0, 4] },
            { text: 'taqin2731@gmail.com  |  +62 851-1782-2731  |  Kabupaten Bogor, Jawa Barat', fontSize: 9, color: GRAY },
            { text: 'github.com/fdciabdul  |  linkedin.com/in/fdciabdul  |  imtaqin.id', fontSize: 9, color: GRAY, margin: [0, 1, 0, 0] },
          ],
        },
      ],
    }

    const docDefinition: any = {
      pageSize: 'A4',
      pageMargins: [40, 40, 40, 40],
      defaultStyle: { font: 'PlusJakartaSans', fontSize: 10, color: DARK, lineHeight: 1.25 },
      content: [
        header,
        rule(),

        h2('Summary'),
        { text: 'Fullstack Developer with 5+ years building production-scale systems — backend APIs, frontend, DevOps, and server infrastructure. Experienced with complex platforms: WhatsApp gateways handling hundreds of thousands of transactions per day, banking automation, a VR application for a national energy company, and monitoring stacks on Grafana and Prometheus. Active in open source with 150+ GitHub repositories and ranked Top 10 freelancer on projects.co.id.' },
        rule(),

        h2('Technical Skills'),
        skill('Languages', 'Rust, Go, TypeScript, JavaScript, PHP, C#, Kotlin, Python'),
        skill('Frontend', 'Vue.js, React Native, Svelte, TailwindCSS'),
        skill('Backend', 'Node.js, AdonisJS, Hono, Laravel, Express'),
        skill('Databases', 'PostgreSQL, MySQL, Redis'),
        skill('DevOps & Cloud', 'Docker, Terraform, Nginx, CI/CD, Grafana, Prometheus'),
        skill('Desktop / Native', 'Tauri, Electron, WebView2, Win32 API'),
        skill('Security', 'Frida, Burp Suite, Metasploit, JADX'),
        rule(),

        h2('Work Experience'),
        job('Software Engineer — Subaga Digital Kreatif', 'Feb 2024 – Present'),
        job('Software Engineer — Namea Solusi Technology', 'Oct 2023 – Jun 2024'),
        job('Backend & DevOps Engineer — PT Kilau Energi Infotama', 'Nov 2022 – May 2024', ['Built backend services and DevOps pipelines, including a VR application for a national energy company.']),
        job('Full Stack Developer — PT Intercity Kerlipan', 'Feb 2021 – Nov 2022'),
        job('WordPress Developer — Claudela', 'Nov 2019 – Jan 2021'),
        job('Full Stack Developer — Wablas.id', 'Oct 2019 – Jun 2020', ['Developed a WhatsApp gateway platform processing high-volume daily messaging traffic.']),
        job('Full Stack Developer — Freelance', 'Jan 2016 – Present', ['Top 10 freelancer on projects.co.id; delivered web, automation, and security projects for clients.']),
        rule(),

        h2('Selected Open-Source Projects'),
        { ul: [
          'CiLocks (2,916 stars) — Android security tool with Metasploit integration.',
          'YOMEN (227 stars) — multi-account YouTube automation bot (Puppeteer).',
          'Frida Multiple Bypass (175 stars) — one-shot SSL pinning, root, and Flutter TLS bypass.',
          'WA-RS — multi-session WhatsApp REST gateway rewritten Node.js to Rust; 8 GB to minimal memory.',
          'Pocket Pentester — 21-module offline Android security toolkit (Rust, Tauri 2).',
          'Tenun — Indonesian-keyword programming language with a compiler written in Zig.',
        ], margin: [0, 0, 0, 6] },
        rule(),

        h2('Education'),
        job('IAIN Laa Roiba — Information Technology', 'Oct 2019 – Mar 2021'),
        job('SMK Pertiwi Cibungbulang — Marketing', 'Jun 2014 – Jun 2017'),
        job('MTs Muallimien Muhammadiyah', 'Jun 2012 – Jun 2014'),
        rule(),

        h2('Awards & Organizations'),
        { ul: [
          'Top 10 Freelancer, projects.co.id — 2026.',
          'Tegal Security — Developer, Jan 2015 – Present (security research community).',
        ], margin: [0, 0, 0, 6] },
        rule(),

        h2('Links'),
        { ul: [
          'Portfolio: porto.imtaqin.id',
          'GitHub: github.com/fdciabdul',
          'LinkedIn: linkedin.com/in/fdciabdul',
          'YouTube: youtube.com/@taqintimur',
        ] },
      ],
    }

    const blob: Blob = await (pdfMake.createPdf(docDefinition) as any).getBlob()
    const url = URL.createObjectURL(blob)
    const a = document.createElement('a')
    a.href = url
    a.download = 'Abdul-Muttaqin-CV.pdf'
    document.body.appendChild(a)
    a.click()
    a.remove()
    setTimeout(() => URL.revokeObjectURL(url), 1000)
  } finally {
    generating.value = false
  }
}
</script>

<template>
  <div class="cv-wrap">
    <!-- screen-only toolbar, hidden when printing -->
    <div class="cv-toolbar no-print">
      <button class="tb-btn" @click="goHome">&larr; Back</button>
      <button class="tb-btn tb-primary" :disabled="generating" @click="downloadPdf">
        {{ generating ? 'Generating…' : 'Download PDF' }}
      </button>
    </div>

    <article class="cv">
      <!-- Header -->
      <header class="cv-head">
        <img class="cv-photo" src="/abdul.jpg" alt="Abdul Muttaqin" />
        <div class="cv-head-text">
          <h1>Abdul Muttaqin</h1>
          <p class="cv-role">Software Engineer &middot; Fullstack Developer</p>
          <p class="cv-contact">
            taqin2731@gmail.com &nbsp;|&nbsp; +62 851-1782-2731 &nbsp;|&nbsp; Kabupaten Bogor, Jawa Barat
          </p>
          <p class="cv-contact">
            github.com/fdciabdul &nbsp;|&nbsp; linkedin.com/in/fdciabdul &nbsp;|&nbsp; imtaqin.id
          </p>
        </div>
      </header>

      <hr />

      <!-- Summary -->
      <section>
        <h2>Summary</h2>
        <p>
          Fullstack Developer with 5+ years building production-scale systems — backend APIs,
          frontend, DevOps, and server infrastructure. Experienced with complex platforms:
          WhatsApp gateways handling hundreds of thousands of transactions per day, banking
          automation, a VR application for a national energy company, and monitoring stacks on
          Grafana and Prometheus. Active in open source with 150+ GitHub repositories and ranked
          Top 10 freelancer on projects.co.id.
        </p>
      </section>

      <hr />

      <!-- Skills -->
      <section>
        <h2>Technical Skills</h2>
        <ul class="cv-skills">
          <li><strong>Languages:</strong> Rust, Go, TypeScript, JavaScript, PHP, C#, Kotlin, Python</li>
          <li><strong>Frontend:</strong> Vue.js, React Native, Svelte, TailwindCSS</li>
          <li><strong>Backend:</strong> Node.js, AdonisJS, Hono, Laravel, Express</li>
          <li><strong>Databases:</strong> PostgreSQL, MySQL, Redis</li>
          <li><strong>DevOps &amp; Cloud:</strong> Docker, Terraform, Nginx, CI/CD, Grafana, Prometheus , OpenStack</li>
          <li><strong>Desktop / Native:</strong> Tauri, Electron, WebView2, Win32 API</li>
          <li><strong>Security:</strong> Frida, Burp Suite, Metasploit, JADX</li>
        </ul>
      </section>

      <hr />

      <!-- Experience -->
      <section>
        <h2>Work Experience</h2>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">Software Engineer &mdash; Subaga Digital Kreatif</span>
            <span class="cv-job-meta">Feb 2024 &ndash; Present</span>
          </div>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">Software Engineer &mdash; Namea Solusi Technology</span>
            <span class="cv-job-meta">Oct 2023 &ndash; Jun 2024</span>
          </div>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">Backend &amp; DevOps Engineer &mdash; PT Kilau Energi Infotama</span>
            <span class="cv-job-meta">Nov 2022 &ndash; May 2024</span>
          </div>
          <ul>
            <li>Built backend services and DevOps pipelines, including a VR application for a national energy company.</li>
          </ul>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">Full Stack Developer &mdash; PT Intercity Kerlipan</span>
            <span class="cv-job-meta">Feb 2021 &ndash; Nov 2022</span>
          </div>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">WordPress Developer &mdash; Claudela</span>
            <span class="cv-job-meta">Nov 2019 &ndash; Jan 2021</span>
          </div>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">Full Stack Developer &mdash; Wablas.id</span>
            <span class="cv-job-meta">Oct 2019 &ndash; Jun 2020</span>
          </div>
          <ul>
            <li>Developed a WhatsApp gateway platform processing high-volume daily messaging traffic.</li>
          </ul>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">Full Stack Developer &mdash; Freelance</span>
            <span class="cv-job-meta">Jan 2016 &ndash; Present</span>
          </div>
          <ul>
            <li>Top 10 freelancer on projects.co.id; delivered web, automation, and security projects for clients.</li>
          </ul>
        </div>
      </section>

      <hr />

      <!-- Selected Open Source -->
      <section>
        <h2>Selected Open-Source Projects</h2>
        <ul class="cv-skills">
          <li><strong>CiLocks</strong> (2,916 stars) — Android security tool with Metasploit integration.</li>
          <li><strong>YOMEN</strong> (227 stars) — multi-account YouTube automation bot (Puppeteer).</li>
          <li><strong>Frida Multiple Bypass</strong> (175 stars) — one-shot SSL pinning, root, and Flutter TLS bypass.</li>
          <li><strong>WA-RS</strong> — multi-session WhatsApp REST gateway rewritten Node.js &rarr; Rust; 8 GB to minimal memory.</li>
          <li><strong>Pocket Pentester</strong> — 21-module offline Android security toolkit (Rust, Tauri 2).</li>
          <li><strong>GoAMPP</strong> — 7 MB native Windows web stack replacing 200 MB XAMPP (Go).</li>
        </ul>
      </section>

      <hr />

      <!-- Education -->
      <section>
        <h2>Education</h2>
        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">IAIN Laa Roiba — Information Technology</span>
            <span class="cv-job-meta">Oct 2019 &ndash; Mar 2021</span>
          </div>
        </div>
        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">SMK Pertiwi Cibungbulang — Marketing</span>
            <span class="cv-job-meta">Jun 2014 &ndash; Jun 2017</span>
          </div>
        </div>
        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">MTs Muallimien Muhammadiyah</span>
            <span class="cv-job-meta">Jun 2012 &ndash; Jun 2014</span>
          </div>
        </div>
      </section>

      <hr />

      <!-- Awards + Org -->
      <section>
        <h2>Awards &amp; Organizations</h2>
        <ul class="cv-skills">
          <li><strong>Top 10 Freelancer</strong>, projects.co.id — 2026.</li>
          <li><strong>Tegal Security</strong> — Developer, Jan 2015 – Present (security research community).</li>
        </ul>
      </section>

      <hr />

      <!-- Links -->
      <section>
        <h2>Links</h2>
        <ul class="cv-skills">
          <li><strong>Portfolio:</strong> porto.imtaqin.id</li>
          <li><strong>GitHub:</strong> github.com/fdciabdul</li>
          <li><strong>LinkedIn:</strong> linkedin.com/in/fdciabdul</li>
          <li><strong>YouTube:</strong> youtube.com/@taqintimur</li>
        </ul>
      </section>
    </article>
  </div>
</template>

<style scoped>
.cv-wrap {
  background: #f4f4f4;
  min-height: 100vh;
  padding: 2rem 1rem 4rem;
}

.cv-toolbar {
  max-width: 800px;
  margin: 0 auto 1.5rem;
  display: flex;
  justify-content: space-between;
  gap: 0.75rem;
}

.tb-btn {
  font-family: Arial, sans-serif;
  font-size: 0.9rem;
  font-weight: 700;
  padding: 0.6rem 1.25rem;
  border: 2px solid #111;
  background: #fff;
  color: #111;
  cursor: pointer;
  box-shadow: 4px 4px 0 #111;
  transition: transform 0.1s, box-shadow 0.1s;
}
.tb-btn:hover {
  transform: translate(-2px, -2px);
  box-shadow: 6px 6px 0 #111;
}
.tb-primary {
  background: #facc15;
}

/* The actual CV document — plain, ATS-friendly */
.cv {
  max-width: 800px;
  margin: 0 auto;
  background: #fff;
  color: #111;
  padding: 3rem 3.25rem;
  font-family: 'Plus Jakarta Sans', Arial, sans-serif;
  font-size: 10.5pt;
  line-height: 1.5;
  box-shadow: 0 2px 18px rgba(0, 0, 0, 0.12);
}

.cv-head {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}
.cv-photo {
  width: 104px;
  height: 104px;
  object-fit: cover;
  object-position: top center;
  border: 2px solid #111;
  flex-shrink: 0;
}
.cv-head-text {
  flex: 1;
}
.cv-head h1 {
  font-size: 24pt;
  font-weight: 700;
  letter-spacing: 0.01em;
  margin: 0;
  line-height: 1;
}
.cv-role {
  font-size: 12pt;
  font-weight: 700;
  margin: 0.15rem 0 0.35rem;
}
.cv-contact {
  font-size: 9.5pt;
  color: #333;
  margin: 0 0 0.15rem;
}

.cv hr {
  border: none;
  border-top: 1px solid #111;
  margin: 1.1rem 0;
}

.cv h2 {
  font-size: 12pt;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin: 0 0 0.6rem;
}

.cv p {
  margin: 0;
}

.cv-skills {
  list-style: none;
  padding: 0;
  margin: 0;
}
.cv-skills li {
  margin-bottom: 0.3rem;
}

.cv-job {
  margin-bottom: 0.75rem;
}
.cv-job:last-child {
  margin-bottom: 0;
}
.cv-job-head {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 1rem;
}
.cv-job-title {
  font-weight: 700;
}
.cv-job-meta {
  font-size: 9.5pt;
  color: #333;
  white-space: nowrap;
}
.cv-job ul {
  margin: 0.2rem 0 0;
  padding-left: 1.1rem;
}
.cv-job li {
  margin-bottom: 0.15rem;
}

/* Print: strip page chrome, full-bleed document */
@media print {
  .no-print {
    display: none !important;
  }
  .cv-wrap {
    background: #fff;
    padding: 0;
  }
  .cv {
    max-width: none;
    box-shadow: none;
    padding: 0.4in 0.6in;
    font-size: 10.5pt;
  }
  .cv-job,
  section {
    page-break-inside: avoid;
  }
}
</style>
