<script setup lang="ts">
import { defineAsyncComponent } from 'vue'
import { Icon } from '@iconify/vue'

const HeroCanvas = defineAsyncComponent(() => import('./HeroCanvas.vue'))

function scrollTo(section: string) {
  const el = document.getElementById(section)
  el?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <section id="hero" class="hero">
    <HeroCanvas />

    <!-- scanline overlay -->
    <div class="scanlines" aria-hidden="true" />

    <!-- horizon divider -->
    <div class="horizon-line" aria-hidden="true" />

    <div class="container hero-inner">
      <div class="hero-left">
        <p class="hero-greeting">Hello, I am</p>
        <h1 class="hero-name">IMTAQIN</h1>

        <div class="hero-role">
          <span class="role-block">Developer</span>
          <span class="role-amp">&amp;</span>
          <span class="role-block">Security Researcher</span>
        </div>

        <p class="hero-desc">
          Building web apps, native tools, and security research.
          Rust, Go, TypeScript, Vue. Based in Indonesia.
        </p>

        <div class="hero-cta">
          <button class="neo-btn neo-btn-primary" @click="scrollTo('projects')">
            View Projects
            <Icon icon="mdi:arrow-right" width="18" />
          </button>
          <button class="neo-btn hero-btn-ghost" @click="scrollTo('contact')">
            Contact Me
          </button>
        </div>

        <div class="hero-stats">
          <div class="stat-card">
            <span class="stat-num">4000+</span>
            <span class="stat-label">GitHub Stars</span>
          </div>
          <div class="stat-card">
            <span class="stat-num">200+</span>
            <span class="stat-label">Repositories</span>
          </div>
          <div class="stat-card">
            <span class="stat-num">4 Orgs</span>
            <span class="stat-label">GitHub Orgs</span>
          </div>
        </div>
      </div>

      <div class="hero-right">
        <div class="avatar-wrap">
          <div class="avatar-label">IMTAQIN.DEV</div>
          <div class="avatar-frame">
            <img src="/avatar.jpg" alt="IMTAQIN" class="avatar-img" />
          </div>
          <div class="avatar-tag">
            <Icon icon="mdi:map-marker" width="14" />
            Indonesia
          </div>
          <div class="avatar-shadow" aria-hidden="true" />
        </div>
      </div>
    </div>

    <button class="scroll-hint" @click="scrollTo('about')" aria-label="Scroll down">
      <Icon icon="mdi:chevron-double-down" width="26" />
    </button>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  background: #000;
  position: relative;
  display: flex;
  align-items: center;
  padding-top: 64px;
  overflow: hidden;
}

/* CRT scanlines overlay */
.scanlines {
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(
    to bottom,
    transparent 0px,
    transparent 2px,
    rgba(0,0,0,0.12) 2px,
    rgba(0,0,0,0.12) 4px
  );
  pointer-events: none;
  z-index: 1;
}

/* Glowing horizon line */
.horizon-line {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 36%;
  height: 1px;
  background: linear-gradient(
    to right,
    transparent 0%,
    rgba(158,255,0,0.6) 20%,
    #9eff00 50%,
    rgba(158,255,0,0.6) 80%,
    transparent 100%
  );
  box-shadow: 0 0 18px 4px rgba(158,255,0,0.25);
  pointer-events: none;
  z-index: 1;
}

.container.hero-inner {
  position: relative;
  z-index: 2;
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 340px;
  gap: 4rem;
  align-items: center;
  padding-top: 3rem;
  padding-bottom: 3rem;
}

/* ─── LEFT ─── */
.hero-left {
  display: flex;
  flex-direction: column;
  gap: 0;
}

.hero-greeting {
  font-size: 0.78rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.25em;
  color: var(--yellow);
  margin-bottom: 0.5rem;
}

.hero-name {
  font-size: clamp(4.5rem, 11vw, 8rem);
  font-weight: 900;
  color: #fff;
  line-height: 0.88;
  text-transform: uppercase;
  letter-spacing: -0.04em;
  margin-bottom: 1.25rem;
  /* text stroke neo-brutalism feel */
  -webkit-text-stroke: 1px rgba(158,255,0,0.15);
}

.hero-role {
  display: flex;
  align-items: center;
  gap: 0.625rem;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
}

.role-block {
  display: inline-block;
  background: var(--yellow);
  color: var(--black);
  font-size: 0.82rem;
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  padding: 0.35rem 0.75rem;
  border: 3px solid var(--black);
}

.role-amp {
  font-size: 0.9rem;
  font-weight: 900;
  color: rgba(255,255,255,0.25);
}

.hero-desc {
  font-size: 0.95rem;
  font-weight: 400;
  color: rgba(255,255,255,0.5);
  max-width: 460px;
  margin-bottom: 2rem;
  line-height: 1.8;
  font-family: Arial, sans-serif;
}

.hero-cta {
  display: flex;
  gap: 0.875rem;
  margin-bottom: 2.5rem;
  flex-wrap: wrap;
}

.hero-btn-ghost {
  background: transparent;
  color: #fff;
  border: 3px solid rgba(255,255,255,0.3);
  box-shadow: 4px 4px 0 rgba(255,255,255,0.1);
}

.hero-btn-ghost:hover {
  border-color: var(--white);
  background: var(--white);
  color: var(--black);
  box-shadow: 6px 6px 0 rgba(255,255,255,0.25);
}

.hero-stats {
  display: flex;
  gap: 2rem;
}

.stat-card {
  display: flex;
  flex-direction: column;
  border-left: 3px solid var(--yellow);
  padding-left: 0.875rem;
}

.stat-num {
  font-size: 1.6rem;
  font-weight: 900;
  color: var(--yellow);
  line-height: 1;
}

.stat-label {
  font-size: 0.65rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: rgba(255,255,255,0.35);
  margin-top: 0.25rem;
}

/* ─── RIGHT / AVATAR ─── */
.hero-right {
  display: flex;
  justify-content: center;
  align-items: center;
}

.avatar-wrap {
  position: relative;
  width: 280px;
}

.avatar-label {
  position: absolute;
  top: -14px;
  left: 12px;
  background: var(--yellow);
  color: var(--black);
  border: 3px solid var(--black);
  font-size: 0.65rem;
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  padding: 0.2rem 0.6rem;
  z-index: 3;
}

.avatar-frame {
  width: 280px;
  height: 320px;
  border: 4px solid var(--yellow);
  overflow: hidden;
  position: relative;
  z-index: 2;
  background: #111;
}

.avatar-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
  filter: contrast(1.05) brightness(0.95);
  display: block;
}

/* Neo-brutalist offset shadow */
.avatar-shadow {
  position: absolute;
  inset: 0;
  border: 4px solid var(--yellow);
  transform: translate(10px, 10px);
  z-index: 1;
  opacity: 0.35;
}

.avatar-tag {
  position: absolute;
  bottom: -14px;
  right: 12px;
  background: var(--black);
  color: var(--yellow);
  border: 3px solid var(--yellow);
  font-size: 0.65rem;
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  padding: 0.2rem 0.6rem;
  display: flex;
  align-items: center;
  gap: 0.25rem;
  z-index: 3;
}

/* scroll hint */
.scroll-hint {
  position: absolute;
  bottom: 1.5rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 3;
  background: none;
  border: 2px solid rgba(255,255,255,0.18);
  color: rgba(255,255,255,0.35);
  padding: 0.4rem;
  cursor: pointer;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: bounce 2s infinite;
  transition: border-color 0.2s, color 0.2s;
}

.scroll-hint:hover {
  border-color: var(--yellow);
  color: var(--yellow);
}

@keyframes bounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50%       { transform: translateX(-50%) translateY(6px); }
}

/* ─── RESPONSIVE ─── */
@media (max-width: 900px) {
  .container.hero-inner {
    grid-template-columns: 1fr;
  }
  .hero-right {
    display: none;
  }
}

@media (max-width: 480px) {
  .hero-cta {
    flex-direction: column;
  }
  .hero-cta .neo-btn {
    width: 100%;
    justify-content: center;
  }
  .hero-stats {
    gap: 1.25rem;
  }
}
</style>
