<script setup lang="ts">
const links = ['Work', 'About', 'Contact']

function scrollTo(id: string) {
  const map: Record<string, string> = { Work: 'projects', About: 'about', Contact: 'contact' }
  document.getElementById(map[id] ?? id.toLowerCase())?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <nav class="nav">
    <div class="container nav-inner">
      <button class="nav-name" @click="scrollTo('hero')">Abdul Muttaqin</button>
      <div class="nav-links">
        <button v-for="l in links" :key="l" @click="scrollTo(l)">{{ l }}</button>
        <a href="#/cv">CV</a>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.nav {
  position: sticky;
  top: 0;
  z-index: 50;
  background: color-mix(in srgb, var(--paper) 88%, transparent);
  backdrop-filter: blur(8px);
}

.nav-inner {
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  gap: 1rem;
  padding-top: 1.5rem;
  padding-bottom: 1.5rem;
}

.nav-name {
  font-family: var(--mono);
  font-size: 0.78rem;
  letter-spacing: 0.02em;
  color: var(--ink);
  padding: 0;
}

.nav-links {
  display: flex;
  gap: 1.5rem;
}

.nav-links button,
.nav-links a {
  font-family: var(--mono);
  font-size: 0.78rem;
  color: var(--muted);
  padding: 0;
  transition: color 0.15s;
}

.nav-links button:hover,
.nav-links a:hover {
  color: var(--ink);
}

@media (max-width: 520px) {
  .nav-links { gap: 1rem; }
  .nav-name { max-width: 8rem; }
}
</style>
