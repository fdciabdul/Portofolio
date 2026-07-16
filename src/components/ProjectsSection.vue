<script setup lang="ts">
import { ref, computed } from 'vue'
import projects from '../data/projects.json'

const activeFilter = ref('All')
const filters = ['All', 'Web', 'Security', 'Automation', 'Native', 'Module', 'Language']

const filtered = computed(() =>
  activeFilter.value === 'All'
    ? (projects as any[])
    : (projects as any[]).filter(p => p.category === activeFilter.value)
)

function countFor(f: string) {
  return f === 'All' ? projects.length : (projects as any[]).filter(p => p.category === f).length
}

function href(p: any) {
  return p.live || p.github || null
}
</script>

<template>
  <section id="projects" class="work">
    <div class="container">
      <span class="eyebrow">Selected work — {{ projects.length }} projects</span>

      <div class="filters">
        <button
          v-for="f in filters"
          :key="f"
          class="filter"
          :class="{ on: activeFilter === f }"
          @click="activeFilter = f"
        >
          {{ f }}<sup>{{ countFor(f) }}</sup>
        </button>
      </div>

      <ul class="rows">
        <li v-for="p in filtered" :key="p.title" class="row">
          <component
            :is="href(p) ? 'a' : 'div'"
            :href="href(p) || undefined"
            :target="href(p) ? '_blank' : undefined"
            rel="noopener"
            class="row-inner"
            :class="{ linked: !!href(p) }"
          >
            <div class="row-main">
              <h3 class="row-title">{{ p.title }}</h3>
              <p class="row-desc">{{ p.description }}</p>
              <p class="row-tags">{{ p.tags.join(' · ') }}</p>
            </div>

            <div class="row-side">
              <span v-if="p.stars" class="stars">{{ p.stars.toLocaleString() }}<i>★</i></span>
              <span class="cat">{{ p.category }}</span>
            </div>
          </component>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>
.filters {
  display: flex;
  flex-wrap: wrap;
  gap: 1.25rem;
  margin-bottom: 3.5rem;
}

.filter {
  font-family: var(--mono);
  font-size: 0.8rem;
  color: var(--muted);
  padding: 0;
  transition: color 0.15s;
}
.filter sup {
  font-size: 0.6rem;
  margin-left: 0.2rem;
  opacity: 0.6;
}
.filter:hover { color: var(--ink); }
.filter.on {
  color: var(--ink);
  background-image: linear-gradient(var(--lime), var(--lime));
  background-repeat: no-repeat;
  background-size: 100% 0.3em;
  background-position: 0 88%;
}

.rows {
  list-style: none;
}

.row + .row {
  border-top: 1px solid var(--rule);
}

.row-inner {
  display: flex;
  gap: 2rem;
  align-items: baseline;
  justify-content: space-between;
  padding: 1.9rem 0;
}

.row-main {
  min-width: 0;
}

.row-title {
  font-family: var(--display);
  font-weight: 700;
  font-size: 1.25rem;
  letter-spacing: -0.02em;
  line-height: 1.2;
  transition: transform 0.2s cubic-bezier(0.2, 0.8, 0.2, 1);
}

.linked:hover .row-title {
  transform: translateX(6px);
}
.linked:hover .row-title::after {
  content: ' ↗';
  font-size: 0.8em;
  color: var(--muted);
}

.row-desc {
  font-size: 0.92rem;
  color: var(--muted);
  margin-top: 0.45rem;
  max-width: 62ch;
}

.row-tags {
  font-family: var(--mono);
  font-size: 0.7rem;
  color: var(--muted);
  opacity: 0.75;
  margin-top: 0.7rem;
}

.row-side {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 0.4rem;
  flex-shrink: 0;
  text-align: right;
}

/* the proof: star counts set as figures */
.stars {
  font-family: var(--display);
  font-weight: 700;
  font-size: 1.35rem;
  letter-spacing: -0.02em;
  line-height: 1;
  white-space: nowrap;
}
.stars i {
  font-style: normal;
  font-size: 0.62em;
  margin-left: 0.15em;
  color: var(--muted);
}

.cat {
  font-family: var(--mono);
  font-size: 0.68rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
}

@media (max-width: 640px) {
  .row-inner {
    flex-direction: column;
    gap: 0.75rem;
    padding: 1.5rem 0;
  }
  .row-side {
    flex-direction: row;
    align-items: baseline;
    gap: 0.75rem;
  }
  .stars { font-size: 1.05rem; }
}
</style>
