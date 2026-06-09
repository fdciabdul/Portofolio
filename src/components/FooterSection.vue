<script setup lang="ts">
import { Icon } from '@iconify/vue'

const year = new Date().getFullYear()

const socials = [
  { icon: 'mdi:github', href: 'https://github.com/fdciabdul', label: 'GitHub' },
  { icon: 'mdi:web', href: 'https://imtaqin.id', label: 'Blog' },
  { icon: 'mdi:email', href: 'mailto:taqin2731@gmail.com', label: 'Email' },
]

function scrollTo(section: string) {
  const el = document.getElementById(section)
  el?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <footer class="footer">
    <div class="container footer-inner">
      <div class="footer-top">
        <div class="footer-brand">
          <span class="footer-logo">IMTAQIN</span>
          <p class="footer-tagline">Building the web, one commit at a time.</p>
        </div>

        <nav class="footer-nav">
          <button @click="scrollTo('about')">About</button>
          <button @click="scrollTo('skills')">Skills</button>
          <button @click="scrollTo('projects')">Projects</button>
          <button @click="scrollTo('contact')">Contact</button>
        </nav>

        <div class="footer-social">
          <a
            v-for="s in socials"
            :key="s.label"
            :href="s.href"
            :aria-label="s.label"
            target="_blank"
            rel="noopener"
            class="social-btn"
          >
            <Icon :icon="s.icon" width="20" />
          </a>
        </div>
      </div>

      <div class="footer-bottom">
        <span>{{ year }} IMTAQIN. All rights reserved.</span>
        <span class="footer-built">
          Built with
          <Icon icon="logos:vue" width="16" style="vertical-align: middle;" />
          Vue.js +
          <Icon icon="logos:vitejs" width="16" style="vertical-align: middle;" />
          Vite
        </span>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: var(--black);
  border-top: 4px solid var(--yellow);
  color: var(--white);
}

.footer-inner {
  padding-top: 3rem;
  padding-bottom: 2rem;
}

.footer-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 2rem;
  padding-bottom: 2rem;
  border-bottom: 2px solid rgba(255,255,255,0.1);
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
}

.footer-logo {
  display: block;
  font-size: 1.75rem;
  font-weight: 900;
  color: var(--yellow);
  letter-spacing: -0.02em;
  margin-bottom: 0.5rem;
}

.footer-tagline {
  font-family: 'Courier New', monospace;
  font-size: 0.85rem;
  color: rgba(255,255,255,0.4);
}

.footer-nav {
  display: flex;
  gap: 0.25rem;
  flex-wrap: wrap;
}

.footer-nav button {
  background: none;
  border: none;
  color: rgba(255,255,255,0.6);
  font-family: inherit;
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  cursor: pointer;
  padding: 0.375rem 0.75rem;
  transition: color 0.1s;
}

.footer-nav button:hover {
  color: var(--yellow);
}

.footer-social {
  display: flex;
  gap: 0.5rem;
}

.social-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 38px;
  height: 38px;
  border: 2px solid rgba(255,255,255,0.2);
  color: rgba(255,255,255,0.6);
  transition: all 0.1s;
}

.social-btn:hover {
  border-color: var(--yellow);
  color: var(--yellow);
  background: rgba(158,255,0,0.05);
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.8rem;
  font-weight: 700;
  color: rgba(255,255,255,0.35);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.footer-built {
  display: flex;
  align-items: center;
  gap: 0.375rem;
}
</style>
