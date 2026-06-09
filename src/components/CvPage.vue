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
        <h1>Abdul Muttaqin</h1>
        <p class="cv-role">Software Developer &amp; Security Researcher</p>
        <p class="cv-contact">
          taqin2731@gmail.com &nbsp;|&nbsp; github.com/fdciabdul &nbsp;|&nbsp; imtaqin.id &nbsp;|&nbsp; Indonesia
        </p>
      </header>

      <hr />

      <!-- Summary -->
      <section>
        <h2>Summary</h2>
        <p>
          Software developer and security researcher with 6+ years building full-stack web
          applications, native desktop tools, and Android security toolkits. Author of open-source
          projects with 4,000+ combined GitHub stars across 200+ repositories. Strong in systems
          programming (Rust, Go), web engineering (TypeScript, Vue), and mobile offensive security.
        </p>
      </section>

      <hr />

      <!-- Skills -->
      <section>
        <h2>Technical Skills</h2>
        <ul class="cv-skills">
          <li><strong>Languages:</strong> Rust, Go, TypeScript, JavaScript, PHP, Kotlin, Python, C#</li>
          <li><strong>Frontend:</strong> Vue.js, React Native, Svelte, TailwindCSS</li>
          <li><strong>Backend:</strong> Node.js, AdonisJS, Hono, Laravel, Express</li>
          <li><strong>Databases:</strong> PostgreSQL, MySQL, Redis, Drizzle ORM, Sequelize</li>
          <li><strong>Desktop / Native:</strong> Tauri, Electron, WebView2, Win32 API</li>
          <li><strong>DevOps:</strong> Docker, Terraform, Nginx, Git</li>
          <li><strong>Security:</strong> Frida, Burp Suite, Metasploit, JADX, HTTP Toolkit, SSL pinning bypass, pentest tooling</li>
        </ul>
      </section>

      <hr />

      <!-- Experience / Selected Work -->
      <section>
        <h2>Selected Projects</h2>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">CiLocks — Android Security Tool</span>
            <span class="cv-job-meta">2,916 stars</span>
          </div>
          <ul>
            <li>Android lockscreen interface crack tool with Metasploit integration and iOS/Android utilities.</li>
            <li>Most-starred project across all maintained accounts.</li>
          </ul>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">YOMEN — YouTube Automation Bot</span>
            <span class="cv-job-meta">227 stars</span>
          </div>
          <ul>
            <li>Multi-account YouTube auto-commenter built with Puppeteer; cookie auth, proxy rotation.</li>
          </ul>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">Frida Multiple Bypass — Mobile Security</span>
            <span class="cv-job-meta">175 stars</span>
          </div>
          <ul>
            <li>One-shot Frida script bypassing SSL pinning, root, emulator, Frida, and Flutter TLS detection simultaneously.</li>
          </ul>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">WA-RS — WhatsApp REST Gateway</span>
            <span class="cv-job-meta">Rust</span>
          </div>
          <ul>
            <li>Multi-session WhatsApp REST API rewritten from Node.js to Rust.</li>
            <li>Cut memory from 8 GB to minimal and eliminated CPU spikes; supports unlimited sessions.</li>
          </ul>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">Pocket Pentester — Native Android Toolkit</span>
            <span class="cv-job-meta">Rust / Tauri 2</span>
          </div>
          <ul>
            <li>21-module offline offensive security toolkit in a 34 MB APK, no root required.</li>
            <li>Port scan, SQLi, XSS, JWT attack, directory fuzzing, and Burp-style repeater.</li>
          </ul>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">GoAMPP — Native Windows Web Stack</span>
            <span class="cv-job-meta">Go</span>
          </div>
          <ul>
            <li>7 MB single-executable Apache + MySQL + PHP stack replacing 200 MB XAMPP.</li>
            <li>No Docker, WSL, or Java required.</li>
          </ul>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">MauBlast &amp; RentalWA — WhatsApp SaaS Platforms</span>
            <span class="cv-job-meta">AdonisJS / Vue / Redis</span>
          </div>
          <ul>
            <li>WhatsApp API gateway and number-rental platforms; multi-session, throttled blast, webhooks.</li>
            <li>Full CRM, Redis queue, and Terraform-provisioned infrastructure.</li>
          </ul>
        </div>

        <div class="cv-job">
          <div class="cv-job-head">
            <span class="cv-job-title">Driver Booster Pro — Native Windows App</span>
            <span class="cv-job-meta">Go / WebView2</span>
          </div>
          <ul>
            <li>Frameless Windows desktop app via Go + WebView2 + direct Win32 API calls; WinUI3 styling.</li>
          </ul>
        </div>
      </section>

      <hr />

      <!-- Other -->
      <section>
        <h2>Additional Open-Source Work</h2>
        <ul class="cv-skills">
          <li>Google Trends Scraper (147 stars) — trending-keyword scraper for SEO.</li>
          <li>mapsdumper (73 stars) — large-scale Google Maps data extractor.</li>
          <li>WareHaus — real-time inventory system (Vue, Hono, Drizzle ORM).</li>
          <li>SHINRAI — AI-powered terminal SSH manager and DevOps agent.</li>
        </ul>
      </section>

      <hr />

      <!-- Links -->
      <section>
        <h2>Links</h2>
        <ul class="cv-skills">
          <li><strong>GitHub:</strong> github.com/fdciabdul</li>
          <li><strong>Portfolio:</strong> porto.imtaqin.id</li>
          <li><strong>Blog:</strong> imtaqin.id</li>
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
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 11pt;
  line-height: 1.5;
  box-shadow: 0 2px 18px rgba(0, 0, 0, 0.12);
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
  margin: 0;
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
  margin-bottom: 0.9rem;
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
