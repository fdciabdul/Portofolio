<script setup lang="ts">
import { ref, computed } from 'vue'
import { Icon } from '@iconify/vue'
import projects from '../data/projects.json'

const activeFilter = ref('All')
const filters = ['All', 'Web', 'Security', 'Automation', 'Native', 'Plugin', 'Language']

const highlighted = computed(() => projects.filter((p: any) => p.highlight))

const filtered = computed(() =>
  activeFilter.value === 'All'
    ? highlighted.value
    : projects.filter((p: any) => p.category === activeFilter.value)
)
</script>

<template>
  <section id="projects" class="projects-section">
    <div class="container">
      <span class="section-label">My Work</span>
      <h2 class="section-title">Projects</h2>

      <div class="filter-row">
        <button
          v-for="f in filters"
          :key="f"
          class="filter-btn"
          :class="{ active: activeFilter === f }"
          @click="activeFilter = f"
        >
          {{ f }}
          <span class="filter-count">
            {{ f === 'All' ? highlighted.length : projects.filter(p => p.category === f).length }}
          </span>
        </button>
        <a href="#/projects-pdf" class="filter-btn pdf-btn">
          <Icon icon="mdi:file-pdf-box" width="16" />
          Export PDF
        </a>
      </div>

      <div class="projects-grid">
        <div
          v-for="project in filtered"
          :key="project.title"
          class="project-card"
        >
          <div class="project-thumb">
            <img
              :src="project.image"
              :alt="project.title"
              class="project-thumb-img"
              loading="lazy"
            />
            <div class="project-thumb-overlay">
              <div class="thumb-badges">
                <span v-if="project.featured" class="badge-featured">
                  <Icon icon="mdi:star" width="11" />
                  Featured
                </span>
                <span class="badge-category" :class="`cat-${project.category.toLowerCase()}`">
                  {{ project.category }}
                </span>
              </div>
              <div v-if="project.stars" class="badge-stars">
                <Icon icon="mdi:star" width="13" />
                {{ project.stars.toLocaleString() }}
              </div>
            </div>
          </div>

          <div class="project-body">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-desc">{{ project.description }}</p>

            <div class="project-tags">
              <span v-for="tag in project.tags" :key="tag" class="project-tag">{{ tag }}</span>
            </div>

            <div class="project-links">
              <a
                v-if="project.github"
                :href="project.github"
                class="project-link"
                target="_blank"
                rel="noopener"
              >
                <Icon icon="mdi:github" width="15" />
                Code
              </a>
              <a
                v-if="project.live"
                :href="project.live"
                class="project-link project-link-solid"
                target="_blank"
                rel="noopener"
              >
                <Icon icon="mdi:open-in-new" width="15" />
                Live
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="github-cta">
        <a href="https://github.com/fdciabdul" target="_blank" rel="noopener" class="neo-btn neo-btn-dark">
          <Icon icon="mdi:github" width="18" /> fdciabdul
        </a>
        <a href="https://github.com/tegal1337" target="_blank" rel="noopener" class="neo-btn neo-btn-dark">
          <Icon icon="mdi:github" width="18" /> tegal1337
        </a>
        <a href="https://github.com/imtaqin" target="_blank" rel="noopener" class="neo-btn neo-btn-dark">
          <Icon icon="mdi:github" width="18" /> imtaqin
        </a>
        <a href="https://github.com/ReverserID" target="_blank" rel="noopener" class="neo-btn neo-btn-dark">
          <Icon icon="mdi:github" width="18" /> ReverserID
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects-section {
  background: var(--bg);
  border-bottom: 3px solid var(--black);
}

.filter-row {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 2.5rem;
  flex-wrap: wrap;
}

.filter-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.5rem 1.125rem;
  font-family: inherit;
  font-size: 0.82rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  border: 2px solid var(--black);
  background: var(--white);
  cursor: pointer;
  box-shadow: 3px 3px 0 var(--black);
  transition: all 0.1s;
  color: var(--black);
}

.filter-btn:hover,
.filter-btn.active {
  background: var(--black);
  color: var(--yellow);
  transform: translate(-2px, -2px);
  box-shadow: 5px 5px 0 var(--black);
}

.filter-count {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 20px;
  height: 20px;
  padding: 0 4px;
  background: rgba(0,0,0,0.1);
  font-size: 0.7rem;
}

.filter-btn.active .filter-count {
  background: rgba(158,255,0,0.2);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: 1.25rem;
  margin-bottom: 3rem;
}

.project-card {
  border: 3px solid var(--black);
  box-shadow: var(--shadow-md);
  background: var(--white);
  display: flex;
  flex-direction: column;
  transition: transform 0.1s, box-shadow 0.1s;
  overflow: hidden;
}

.project-card:hover {
  transform: translate(-4px, -4px);
  box-shadow: 9px 9px 0 var(--black);
}

.project-thumb {
  position: relative;
  height: 195px;
  overflow: hidden;
  border-bottom: 3px solid var(--black);
  background: #e8e8e8;
}

.project-thumb-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top;
  display: block;
  transition: transform 0.35s;
}

.project-card:hover .project-thumb-img {
  transform: scale(1.04);
}

.project-thumb-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(0,0,0,0.55) 0%,
    transparent 35%,
    transparent 65%,
    rgba(0,0,0,0.35) 100%
  );
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  padding: 0.625rem;
}

.thumb-badges {
  display: flex;
  flex-direction: column;
  gap: 0.3rem;
}

.badge-featured {
  display: inline-flex;
  align-items: center;
  gap: 0.2rem;
  background: var(--lime);
  color: var(--black);
  border: 2px solid var(--black);
  padding: 0.15rem 0.45rem;
  font-size: 0.62rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.badge-category {
  display: inline-block;
  padding: 0.15rem 0.45rem;
  font-size: 0.62rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  border: 2px solid var(--black);
}

.cat-web { background: var(--sky); color: var(--black); }
.cat-security { background: var(--coral); color: var(--white); }
.cat-automation { background: var(--yellow); color: var(--black); }
.cat-native { background: var(--lime); color: var(--black); }
.cat-plugin { background: var(--purple); color: var(--black); }
.cat-language { background: #b5651d; color: var(--white); }

.pdf-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  margin-left: auto;
  background: var(--black);
  color: var(--yellow);
  text-decoration: none;
}
.pdf-btn:hover { background: var(--yellow); color: var(--black); }

.badge-stars {
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
  background: var(--yellow);
  color: var(--black);
  border: 2px solid var(--black);
  padding: 0.2rem 0.45rem;
  font-size: 0.72rem;
  font-weight: 700;
  align-self: flex-start;
}

.project-body {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  padding: 1.25rem;
  flex: 1;
}

.project-title {
  font-size: 1.1rem;
  font-weight: 900;
  text-transform: uppercase;
  line-height: 1.1;
}

.project-desc {
  font-family: Arial, sans-serif;
  font-size: 0.865rem;
  font-weight: 400;
  line-height: 1.65;
  color: #333;
  flex: 1;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.35rem;
}

.project-tag {
  font-size: 0.68rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  border: 2px solid var(--black);
  background: var(--bg);
  padding: 0.18rem 0.45rem;
}

.project-links {
  display: flex;
  gap: 0.5rem;
  padding-top: 0.75rem;
  border-top: 2px solid var(--black);
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 0.3rem;
  font-size: 0.76rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  border: 2px solid var(--black);
  padding: 0.375rem 0.75rem;
  background: var(--bg);
  box-shadow: 2px 2px 0 var(--black);
  transition: all 0.1s;
  color: var(--black);
}

.project-link:hover {
  transform: translate(-1px, -1px);
  box-shadow: 3px 3px 0 var(--black);
  background: var(--black);
  color: var(--yellow);
}

.project-link-solid {
  background: var(--black);
  color: var(--yellow);
  box-shadow: 2px 2px 0 #555;
}

.project-link-solid:hover {
  background: #111;
  box-shadow: 3px 3px 0 #555;
  transform: translate(-1px, -1px);
}

.github-cta {
  display: flex;
  justify-content: center;
  gap: 0.75rem;
  flex-wrap: wrap;
}

@media (max-width: 640px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>
