<script setup lang="ts">
const stats = [
  { value: '4,000+', label: 'GitHub stars' },
  { value: '200+', label: 'Repositories' },
  { value: '5 yrs', label: 'In production' },
]

function scrollTo(id: string) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <section id="hero" class="hero">
    <div class="container">
      <h1 class="hero-line">
        I build web apps, developer tools, and
        <span class="mark">one programming language</span>.
      </h1>

      <p class="hero-body">
        Abdul Muttaqin — software engineer and security researcher, based in Indonesia.
        Five years shipping WhatsApp gateways at national scale, AI customer-service
        platforms, native desktop tools, and Android security research. I also wrote a
        programming language whose keywords are Indonesian.
      </p>

      <dl class="hero-stats">
        <div v-for="s in stats" :key="s.label" class="stat">
          <dt>{{ s.value }}</dt>
          <dd>{{ s.label }}</dd>
        </div>
      </dl>

      <div class="hero-actions">
        <button class="link-underline" @click="scrollTo('projects')">See the work</button>
        <a class="link-underline" href="#/cv">Read the CV</a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  padding-top: 6rem;
  padding-bottom: 5rem;
}

.hero-line {
  font-family: var(--display);
  font-weight: 800;
  font-size: clamp(2.6rem, 7.4vw, 4.6rem);
  line-height: 1.02;
  letter-spacing: -0.035em;
  max-width: 15ch;
  margin-bottom: 2rem;
  animation: rise 0.7s cubic-bezier(0.2, 0.8, 0.2, 1) both;
}

.hero-body {
  font-size: 1.05rem;
  color: var(--muted);
  max-width: 58ch;
  margin-bottom: 3rem;
  animation: rise 0.7s 0.08s cubic-bezier(0.2, 0.8, 0.2, 1) both;
}

.hero-stats {
  display: flex;
  gap: 3rem;
  margin-bottom: 2.5rem;
  animation: rise 0.7s 0.16s cubic-bezier(0.2, 0.8, 0.2, 1) both;
}

.stat dt {
  font-family: var(--display);
  font-weight: 700;
  font-size: 1.6rem;
  letter-spacing: -0.02em;
  line-height: 1;
}

.stat dd {
  font-family: var(--mono);
  font-size: 0.7rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
  margin-top: 0.4rem;
}

.hero-actions {
  display: flex;
  gap: 2rem;
  font-family: var(--mono);
  font-size: 0.82rem;
  animation: rise 0.7s 0.24s cubic-bezier(0.2, 0.8, 0.2, 1) both;
}

@keyframes rise {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: none; }
}

@media (max-width: 640px) {
  .hero { padding-top: 3rem; }
  .hero-stats { gap: 1.75rem; }
  .stat dt { font-size: 1.3rem; }
}
</style>
