<script setup lang="ts">
function goHome() {
  window.location.hash = ''
}
function downloadPdf() {
  window.print()
}
</script>

<template>
  <div class="cv-wrap">
    <!-- screen-only toolbar, hidden when printing -->
    <div class="cv-toolbar no-print">
      <button class="tb-btn" @click="goHome">&larr; Back</button>
      <button class="tb-btn tb-primary" @click="downloadPdf">Download PDF</button>
    </div>

    <article class="cv">
      <!-- Header -->
      <header class="cv-head">
        <img class="cv-photo" src="/abdul.jpg" alt="Abdul Muttaqin" />
        <div class="cv-head-text">
          <h1>Abdul Muttaqin</h1>
          <p class="cv-role">Software Engineer &middot; Fullstack Developer</p>
          <p class="cv-contact">
            taqin2731@gmail.com &nbsp;|&nbsp; +62 851-1782-2731 &nbsp;|&nbsp; Jakarta Selatan, DKI Jakarta
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
          <li><strong>DevOps &amp; Cloud:</strong> Docker, Terraform, Nginx, CI/CD, Grafana, Prometheus</li>
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
  width: 92px;
  height: 92px;
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
