<script setup lang="ts">
import { Icon } from '@iconify/vue'
</script>

<template>
  <section id="about" class="about-section">
    <div class="container">
      <div class="about-grid">
        <div class="about-left">
          <span class="section-label">About Me</span>
          <h2 class="section-title">Who Am I?</h2>

          <div class="about-text">
            <p>
              Developer and security researcher. I build full-stack web
              apps, native desktop tools, and Android security toolkits.
              I write in Rust, Go, TypeScript, and Vue.
            </p>
            <p>
              Creator of WA-RS (multi-session WhatsApp gateway in Rust),
              Pocket Pentester (native Android security toolkit), and
              several open-source tools with 400+ GitHub stars combined.
            </p>
          </div>

          <div class="about-details">
            <div class="detail-item">
              <Icon icon="mdi:map-marker" width="20" />
              <span>Indonesia</span>
            </div>
            <div class="detail-item">
              <Icon icon="mdi:email" width="20" />
              <span>taqin2731@gmail.com</span>
            </div>
            <div class="detail-item">
              <Icon icon="mdi:github" width="20" />
              <span>github.com/fdciabdul</span>
            </div>
            <div class="detail-item">
              <Icon icon="mdi:web" width="20" />
              <span>imtaqin.id</span>
            </div>
          </div>

          <a href="#/cv" class="neo-btn neo-btn-primary" style="margin-top: 2rem; display: inline-flex;">
            <Icon icon="mdi:file-document-outline" width="18" />
            View CV / Resume
          </a>
        </div>

        <div class="about-right">
          <div class="services-grid">
            <div class="service-card service-yellow">
              <div class="service-icon">
                <Icon icon="mdi:monitor-dashboard" width="32" />
              </div>
              <h3>Web Dev</h3>
              <p>Vue.js, TypeScript, Node.js, REST APIs</p>
            </div>
            <div class="service-card service-white">
              <div class="service-icon">
                <Icon icon="mdi:desktop-tower" width="32" />
              </div>
              <h3>Desktop Apps</h3>
              <p>Rust, Go, Tauri, Electron, WebView2, Win32 API</p>
            </div>
            <div class="service-card service-lime">
              <div class="service-icon">
                <Icon icon="mdi:cellphone" width="32" />
              </div>
              <h3>Mobile Apps</h3>
              <p>Kotlin, React Native, Tauri Android, Android SDK</p>
            </div>
            <div class="service-card service-sky">
              <div class="service-icon">
                <Icon icon="mdi:shield-bug" width="32" />
              </div>
              <h3>Security</h3>
              <p>Frida, SSL bypass, pentest tooling, Android</p>
            </div>
            <div class="service-card service-coral">
              <div class="service-icon">
                <Icon icon="mdi:robot" width="32" />
              </div>
              <h3>Automation</h3>
              <p>WhatsApp bots, AI agents, scrapers</p>
            </div>
            <div class="service-card service-purple">
              <div class="service-icon">
                <Icon icon="mdi:server-network" width="32" />
              </div>
              <h3>DevOps</h3>
              <p>Docker, Terraform, Nginx, CI/CD</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-section {
  background: var(--white);
  border-top: 3px solid var(--black);
  border-bottom: 3px solid var(--black);
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5rem;
  align-items: start;
}

.about-text {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2rem;
  font-size: 1.05rem;
  font-family: Arial, sans-serif;
  font-weight: 400;
  line-height: 1.75;
  color: #333;
}

.about-details {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  border: 3px solid var(--black);
  padding: 1.25rem;
  box-shadow: var(--shadow-md);
  background: var(--bg);
}

.detail-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-size: 0.9rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.03em;
}

.services-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.service-card {
  border: 3px solid var(--black);
  padding: 1.5rem;
  box-shadow: var(--shadow-md);
  transition: transform 0.1s, box-shadow 0.1s;
}

.service-card:hover {
  transform: translate(-3px, -3px);
  box-shadow: 8px 8px 0 var(--black);
}

.service-yellow { background: var(--yellow); }
.service-white { background: var(--white); }
.service-lime { background: var(--lime); }
.service-sky { background: var(--sky); }
.service-coral { background: var(--coral); }
.service-purple { background: var(--purple); }

.service-icon {
  margin-bottom: 0.75rem;
}

.service-card h3 {
  font-size: 1rem;
  font-weight: 900;
  text-transform: uppercase;
  margin-bottom: 0.5rem;
}

.service-card p {
  font-family: Arial, sans-serif;
  font-size: 0.85rem;
  font-weight: 400;
  line-height: 1.5;
  color: #333;
}

@media (max-width: 900px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}

@media (max-width: 520px) {
  .services-grid {
    grid-template-columns: 1fr;
  }
}
</style>
