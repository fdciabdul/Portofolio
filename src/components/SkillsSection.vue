<script setup lang="ts">
import { Icon } from '@iconify/vue'

const CDN = 'https://icon.icepanel.io/Technology/svg'

const groups = [
  {
    label: 'Languages',
    color: 'yellow',
    icon: 'mdi:code-braces',
    items: [
      { name: 'TypeScript', img: `${CDN}/TypeScript.svg` },
      { name: 'JavaScript', img: `${CDN}/JavaScript.svg` },
      { name: 'Rust', img: `${CDN}/Rust.svg` },
      { name: 'Go', img: `${CDN}/Go.svg` },
      { name: 'PHP', img: `${CDN}/PHP.svg` },
      { name: 'Kotlin', img: `${CDN}/Kotlin.svg` },
      { name: 'Python', img: `${CDN}/Python.svg` },
      { name: 'C#', img: `https://upload.wikimedia.org/wikipedia/commons/3/3c/Logo_C_sharp.png` },
    ],
  },
  {
    label: 'Frontend & Desktop',
    color: 'sky',
    icon: 'mdi:monitor',
    items: [
      { name: 'Vue.js', img: `${CDN}/Vue.js.svg` },
      { name: 'Tauri', img: `${CDN}/Tauri.svg` },
      { name: 'Electron', img: `${CDN}/Electron.svg` },
      { name: 'React Native', img: `${CDN}/React.svg` },
      { name: 'Svelte', img: `${CDN}/Svelte.svg` },
      { name: 'TailwindCSS', img: `${CDN}/Tailwind-CSS.svg` },
      { name: 'WebView2', img: `${CDN}/Windows-11.svg` },
      { name: 'Win32 API', img: `${CDN}/Windows-11.svg` },
    ],
  },
  {
    label: 'Backend',
    color: 'lime',
    icon: 'mdi:server',
    items: [
      { name: 'Node.js', img: `${CDN}/Node.js.svg` },
      { name: 'Adonis.js', img: `${CDN}/AdonisJS.svg` },
      { name: 'Hono', img: null, iconFallback: 'logos:hono' },
      { name: 'Laravel', img: `${CDN}/Laravel.svg` },
      { name: 'Express', img: `${CDN}/Express.svg` },
    ],
  },
  {
    label: 'Database & Infra',
    color: 'coral',
    icon: 'mdi:database',
    items: [
      { name: 'PostgreSQL', img: `${CDN}/PostgresSQL.svg` },
      { name: 'MySQL', img: `${CDN}/MySQL.svg` },
      { name: 'Redis', img: `${CDN}/Redis.svg` },
      { name: 'Drizzle ORM', img: null, iconFallback: 'logos:drizzle-orm' },
      { name: 'Sequelize', img: `${CDN}/Sequelize.svg` },
      { name: 'Docker', img: `${CDN}/Docker.svg` },
      { name: 'Terraform', img: `${CDN}/HashiCorp-Terraform.svg` },
      { name: 'Nginx', img: `${CDN}/NGINX.svg` },
    ],
  },
  {
    label: 'Security & Reverse',
    color: 'purple',
    icon: 'mdi:shield-bug',
    items: [
      { name: 'Frida', img: null, iconFallback: 'mdi:bug-outline' },
      { name: 'Burp Suite', img: `https://assets.tryhackme.com/img/modules/burp-suite.png`, iconFallback: 'mdi:web-check' },
      { name: 'HTTP Toolkit', img: `https://avatars.githubusercontent.com/u/39777515?s=200&v=4`, iconFallback: 'mdi:web' },
      { name: 'Metasploit', img: `https://gdm-catalog-fmapi-prod.imgix.net/ProductLogo/17df60fe-5944-44ad-b73a-531294eea4a0.png?w=80&h=80&fit=max&dpr=3&auto=format&q=50`, iconFallback: 'mdi:skull-outline' },
      { name: 'Android', img: `${CDN}/Android.svg` },
      { name: 'Puppeteer', img: `https://user-images.githubusercontent.com/10379601/29446482-04f7036a-841f-11e7-9872-91d1fc2ea683.png` },
      { name: 'JADX', img: `https://raw.githubusercontent.com/skylot/jadx/master/jadx-gui/src/main/resources/logos/jadx-logo.png`, iconFallback: 'mdi:android' },
    ],
  },
]

const colorMap: Record<string, string> = {
  yellow: 'var(--yellow)',
  sky: 'var(--sky)',
  lime: 'var(--lime)',
  coral: 'var(--coral)',
  purple: 'var(--purple)',
}
</script>

<template>
  <section id="skills" class="skills-section">
    <div class="container">
      <span class="section-label">What I Use</span>
      <h2 class="section-title">Tech Stack</h2>

      <div class="groups-grid">
        <div
          v-for="group in groups"
          :key="group.label"
          class="skill-group"
          :style="{ '--group-color': colorMap[group.color] }"
        >
          <div class="group-header">
            <div class="group-icon">
              <Icon :icon="group.icon" width="18" />
            </div>
            <span class="group-label">{{ group.label }}</span>
          </div>

          <div class="skill-tags">
            <div
              v-for="item in group.items"
              :key="item.name"
              class="skill-tag"
            >
              <img
                v-if="item.img"
                :src="item.img"
                :alt="item.name"
                class="skill-icon-img"
                width="16"
                height="16"
                loading="lazy"
              />
              <Icon
                v-else-if="item.iconFallback"
                :icon="item.iconFallback"
                width="16"
                height="16"
              />
              <span>{{ item.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills-section {
  background: var(--yellow);
  border-bottom: 3px solid var(--black);
}

.groups-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 1.125rem;
}

.skill-group {
  background: var(--white);
  border: 3px solid var(--black);
  box-shadow: var(--shadow-md);
  overflow: hidden;
  transition: transform 0.1s, box-shadow 0.1s;
}

.skill-group:hover {
  transform: translate(-3px, -3px);
  box-shadow: 8px 8px 0 var(--black);
}

.group-header {
  display: flex;
  align-items: center;
  gap: 0.625rem;
  padding: 0.75rem 1rem;
  background: var(--group-color);
  border-bottom: 3px solid var(--black);
}

.group-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 30px;
  height: 30px;
  background: var(--black);
  color: var(--group-color);
  flex-shrink: 0;
}

.group-label {
  font-size: 0.8rem;
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  padding: 1rem;
}

.skill-tag {
  display: inline-flex;
  align-items: center;
  gap: 0.375rem;
  border: 2px solid var(--black);
  background: var(--bg);
  padding: 0.35rem 0.7rem;
  font-size: 0.78rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  box-shadow: 2px 2px 0 var(--black);
  transition: all 0.1s;
  cursor: default;
}

.skill-tag:hover {
  background: var(--group-color);
  transform: translate(-1px, -1px);
  box-shadow: 3px 3px 0 var(--black);
}

.skill-icon-img {
  display: block;
  object-fit: contain;
  flex-shrink: 0;
}

@media (max-width: 600px) {
  .groups-grid {
    grid-template-columns: 1fr;
  }
}
</style>
