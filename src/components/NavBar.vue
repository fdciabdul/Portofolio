<script setup lang="ts">
import { ref } from 'vue'
import { Icon } from '@iconify/vue'

const menuOpen = ref(false)
const navLinks = ['About', 'Skills', 'Projects', 'Contact']

function scrollTo(section: string) {
  const el = document.getElementById(section.toLowerCase())
  el?.scrollIntoView({ behavior: 'smooth' })
  menuOpen.value = false
}
</script>

<template>
  <nav class="navbar">
    <div class="container nav-inner">
      <button class="nav-logo" @click="scrollTo('hero')">IMTAQIN</button>

      <ul class="nav-links">
        <li v-for="link in navLinks" :key="link">
          <button class="nav-link-btn" @click="scrollTo(link)">{{ link }}</button>
        </li>
      </ul>

      <div class="nav-actions">
        <a href="https://github.com/fdciabdul" target="_blank" rel="noopener" class="neo-icon-btn" aria-label="GitHub">
          <Icon icon="mdi:github" width="22" />
        </a>
        <a href="https://imtaqin.id" target="_blank" rel="noopener" class="neo-icon-btn" aria-label="Blog">
          <Icon icon="mdi:web" width="22" />
        </a>
      </div>

      <button class="hamburger" @click="menuOpen = !menuOpen" aria-label="Toggle menu">
        <Icon :icon="menuOpen ? 'mdi:close' : 'mdi:menu'" width="26" />
      </button>
    </div>

    <div class="mobile-menu" :class="{ open: menuOpen }">
      <ul>
        <li v-for="link in navLinks" :key="link">
          <button class="mobile-nav-btn" @click="scrollTo(link)">{{ link }}</button>
        </li>
      </ul>
      <div class="mobile-social">
        <a href="https://github.com/fdciabdul" target="_blank" rel="noopener" class="neo-icon-btn">
          <Icon icon="mdi:github" width="22" />
        </a>
        <a href="https://imtaqin.id" target="_blank" rel="noopener" class="neo-icon-btn">
          <Icon icon="mdi:web" width="22" />
        </a>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  background: var(--yellow);
  border-bottom: 3px solid var(--black);
}

.nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 64px;
}

.nav-logo {
  font-size: 1.25rem;
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: -0.02em;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  color: var(--black);
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 0.125rem;
}

.nav-link-btn {
  background: none;
  border: 2px solid transparent;
  font-size: 0.875rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  cursor: pointer;
  padding: 0.4rem 0.875rem;
  color: var(--black);
  transition: all 0.1s;
}

.nav-link-btn:hover {
  border-color: var(--black);
  background: var(--black);
  color: var(--yellow);
}

.nav-actions {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}

.neo-icon-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 38px;
  height: 38px;
  border: 2px solid var(--black);
  background: var(--white);
  box-shadow: var(--shadow-sm);
  transition: transform 0.1s, box-shadow 0.1s;
  color: var(--black);
}

.neo-icon-btn:hover {
  transform: translate(-2px, -2px);
  box-shadow: 5px 5px 0 var(--black);
}

.hamburger {
  display: none;
  align-items: center;
  justify-content: center;
  background: var(--black);
  border: none;
  color: var(--yellow);
  padding: 0.375rem;
  cursor: pointer;
  width: 38px;
  height: 38px;
}

.mobile-menu {
  display: none;
  background: var(--yellow);
  border-top: 2px solid var(--black);
  padding: 1.25rem 1.5rem;
}

.mobile-menu.open {
  display: block;
}

.mobile-menu ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.375rem;
  margin-bottom: 1rem;
}

.mobile-nav-btn {
  width: 100%;
  background: var(--white);
  border: 2px solid var(--black);
  padding: 0.75rem 1rem;
  font-family: inherit;
  font-size: 0.9rem;
  font-weight: 700;
  text-transform: uppercase;
  text-align: left;
  cursor: pointer;
  box-shadow: var(--shadow-sm);
  transition: all 0.1s;
  color: var(--black);
}

.mobile-nav-btn:hover {
  background: var(--black);
  color: var(--yellow);
}

.mobile-social {
  display: flex;
  gap: 0.5rem;
}

@media (max-width: 768px) {
  .nav-links,
  .nav-actions {
    display: none;
  }

  .hamburger {
    display: flex;
  }
}
</style>
