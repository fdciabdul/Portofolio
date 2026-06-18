<script setup lang="ts">
import { computed } from 'vue'
import projects from '../data/projects.json'

const ORDER = ['Language', 'Plugin', 'Web', 'Security', 'Automation', 'Native']

const grouped = computed(() => {
  const map: Record<string, any[]> = {}
  for (const p of projects as any[]) {
    (map[p.category] ||= []).push(p)
  }
  return ORDER
    .filter(c => map[c]?.length)
    .map(c => ({ category: c, items: map[c]! }))
})

function cleanUrl(u: string | null) {
  if (!u) return ''
  return u.replace(/^https?:\/\//, '').replace(/\/$/, '')
}

function goHome() {
  window.location.hash = ''
}
function downloadPdf() {
  window.print()
}
</script>

<template>
  <div class="pd-wrap">
    <div class="pd-toolbar no-print">
      <button class="tb-btn" @click="goHome">&larr; Back</button>
      <button class="tb-btn tb-primary" @click="downloadPdf">Download PDF</button>
    </div>

    <article class="pd">
      <header class="pd-head">
        <h1>Abdul Muttaqin — Project Portfolio</h1>
        <p class="pd-sub">
          Software Engineer &middot; Fullstack Developer &nbsp;|&nbsp;
          github.com/fdciabdul &nbsp;|&nbsp; porto.imtaqin.id
        </p>
      </header>

      <hr />

      <section v-for="group in grouped" :key="group.category" class="pd-group">
        <h2>{{ group.category }}</h2>

        <div v-for="p in group.items" :key="p.title" class="pd-item">
          <div class="pd-item-head">
            <span class="pd-title">{{ p.title }}</span>
            <span v-if="p.stars" class="pd-meta">{{ p.stars }} stars</span>
          </div>
          <p class="pd-desc">{{ p.description }}</p>
          <p class="pd-tags">{{ p.tags.join(' · ') }}</p>
          <p v-if="p.github || p.live" class="pd-links">
            <span v-if="p.github">{{ cleanUrl(p.github) }}</span>
            <span v-if="p.github && p.live"> &nbsp;|&nbsp; </span>
            <span v-if="p.live">{{ cleanUrl(p.live) }}</span>
          </p>
        </div>
      </section>
    </article>
  </div>
</template>

<style scoped>
.pd-wrap {
  background: #f4f4f4;
  min-height: 100vh;
  padding: 2rem 1rem 4rem;
}
.pd-toolbar {
  max-width: 820px;
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
.tb-btn:hover { transform: translate(-2px, -2px); box-shadow: 6px 6px 0 #111; }
.tb-primary { background: #9eff00; }

.pd {
  max-width: 820px;
  margin: 0 auto;
  background: #fff;
  color: #111;
  padding: 2.75rem 3rem;
  font-family: 'Plus Jakarta Sans', Arial, sans-serif;
  font-size: 10.5pt;
  line-height: 1.5;
  box-shadow: 0 2px 18px rgba(0,0,0,0.12);
}

.pd-head h1 { font-size: 19pt; font-weight: 800; margin: 0; }
.pd-sub { font-size: 9pt; color: #444; margin: 0.3rem 0 0; }

.pd hr { border: none; border-top: 1px solid #111; margin: 1rem 0; }

.pd-group { margin-bottom: 1.4rem; }
.pd-group h2 {
  font-size: 11pt;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  border-bottom: 2px solid #9eff00;
  padding-bottom: 0.2rem;
  margin: 0 0 0.7rem;
}

.pd-item {
  margin-bottom: 0.85rem;
  page-break-inside: avoid;
}
.pd-item-head {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 1rem;
}
.pd-title { font-weight: 700; font-size: 11pt; }
.pd-meta { font-size: 9pt; color: #555; white-space: nowrap; }
.pd-desc { margin: 0.15rem 0 0.2rem; }
.pd-tags { margin: 0; font-size: 9pt; color: #555; font-weight: 600; }
.pd-links { margin: 0.1rem 0 0; font-size: 9pt; color: #333; }

@media print {
  .no-print { display: none !important; }
  .pd-wrap { background: #fff; padding: 0; }
  .pd { max-width: none; box-shadow: none; padding: 0.4in 0.55in; font-size: 10pt; }
  .pd-group { page-break-inside: auto; }
}
</style>
