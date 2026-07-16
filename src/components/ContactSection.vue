<script setup lang="ts">
const links = [
  { label: 'Email', value: 'taqin2731@gmail.com', href: 'mailto:taqin2731@gmail.com' },
  { label: 'GitHub', value: 'github.com/fdciabdul', href: 'https://github.com/fdciabdul' },
  { label: 'LinkedIn', value: 'linkedin.com/in/fdciabdul', href: 'https://www.linkedin.com/in/fdciabdul' },
  { label: 'Writing', value: 'imtaqin.id', href: 'https://imtaqin.id' },
]
</script>

<template>
  <section id="contact" class="contact">
    <div class="container">
      <span class="eyebrow">Contact</span>

      <h2 class="contact-line">
        Got something that needs to
        <span class="mark">actually ship</span>?
      </h2>

      <p class="contact-body">
        Open to full-time roles, contract work, and freelance projects — remote or around
        Jakarta. I usually reply within a day.
      </p>

      <ul class="links">
        <li v-for="l in links" :key="l.label">
          <a :href="l.href" target="_blank" rel="noopener" class="link">
            <span class="link-label">{{ l.label }}</span>
            <span class="link-value">{{ l.value }}</span>
            <span class="link-arrow" aria-hidden="true">↗</span>
          </a>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>
.contact-line {
  font-family: var(--display);
  font-weight: 800;
  font-size: clamp(2rem, 5.4vw, 3.2rem);
  line-height: 1.06;
  letter-spacing: -0.03em;
  max-width: 16ch;
  margin-bottom: 1.5rem;
}

.contact-body {
  font-size: 1.05rem;
  color: var(--muted);
  max-width: 54ch;
  margin-bottom: 3rem;
}

.links {
  list-style: none;
}

.links li { border-top: 1px solid var(--rule); }
.links li:last-child { border-bottom: 1px solid var(--rule); }

.link {
  display: flex;
  align-items: baseline;
  gap: 1.5rem;
  padding: 1.1rem 0;
}

.link-label {
  font-family: var(--mono);
  font-size: 0.72rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
  width: 7.5rem;
  flex-shrink: 0;
}

.link-value {
  font-size: 1rem;
  transition: transform 0.2s cubic-bezier(0.2, 0.8, 0.2, 1);
}

.link-arrow {
  margin-left: auto;
  color: var(--muted);
  opacity: 0;
  transition: opacity 0.2s;
}

.link:hover .link-value { transform: translateX(5px); }
.link:hover .link-arrow { opacity: 1; }

@media (max-width: 640px) {
  .link { gap: 0.75rem; }
  .link-label { width: 5.5rem; }
  .link-value { font-size: 0.9rem; }
}
</style>
