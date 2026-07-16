<script setup lang="ts">
const stack = [
  { label: 'Languages', items: 'Rust · Go · TypeScript · JavaScript · PHP · Kotlin · Python · C#' },
  { label: 'Frontend', items: 'Vue.js · Svelte · React Native · TailwindCSS' },
  { label: 'Backend', items: 'Node.js · Hono · AdonisJS · Laravel · Express' },
  { label: 'Data', items: 'PostgreSQL · MySQL · Redis · Drizzle · pgvector' },
  { label: 'Infra', items: 'Docker · Terraform · Nginx · Grafana · Prometheus' },
  { label: 'Desktop', items: 'Tauri · Electron · WebView2 · Win32 API' },
  { label: 'Security', items: 'Frida · Burp Suite · Metasploit · JADX' },
]
</script>

<template>
  <section id="about" class="about">
    <div class="container">
      <span class="eyebrow">About</span>

      <div class="prose">
        <p>
          I started freelancing in 2016 and never really stopped. Since then I've built
          WhatsApp gateways that move hundreds of thousands of messages a day, an AI
          customer-service platform for a motorcycle workshop chain, a PPOB payments
          platform, and a VR application for a national energy company.
        </p>
        <p>
          The other half of my work is security research — Android tooling, SSL pinning
          bypasses, and offensive toolkits. Roughly 200 repositories and
          <span class="mark">4,000+ GitHub stars</span> came out of that habit.
        </p>
        <p>
          Somewhere in between, I wrote <a class="link-underline" href="https://github.com/TenunLang/Tenun" target="_blank" rel="noopener">Tenun</a> —
          a statically typed programming language whose keywords are Indonesian, with a
          compiler in Zig and three execution backends. It looks like this:
        </p>
      </div>

      <pre class="artifact"><code>fungsi salam(nama: teks): kosong {
    cetak("Halo, " + nama);
}

biar angka: bulat = 10;

<span class="kw">kalau</span> angka > 5 {
    salam("Tenun");
} <span class="kw">lain</span> {
    cetak("kecil");
}</code></pre>

      <div class="stack">
        <div v-for="s in stack" :key="s.label" class="stack-row">
          <span class="stack-label">{{ s.label }}</span>
          <span class="stack-items">{{ s.items }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.prose p {
  font-size: 1.05rem;
  max-width: 62ch;
  margin-bottom: 1.25rem;
}
.prose p:last-child { margin-bottom: 0; }

/* his own language, shown as the artifact it is */
.artifact {
  font-family: var(--mono);
  font-size: 0.8rem;
  line-height: 1.75;
  color: var(--ink);
  background: #F2F2EE;
  padding: 1.5rem 1.5rem;
  margin: 2.25rem 0 3.5rem;
  overflow-x: auto;
  white-space: pre;
}
.artifact .kw {
  background-image: linear-gradient(var(--lime), var(--lime));
  background-repeat: no-repeat;
  background-size: 100% 0.9em;
  background-position: 0 62%;
}

.stack-row {
  display: flex;
  gap: 1.5rem;
  padding: 0.85rem 0;
  border-top: 1px solid var(--rule);
}
.stack-row:last-child { border-bottom: 1px solid var(--rule); }

.stack-label {
  font-family: var(--mono);
  font-size: 0.72rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
  width: 7.5rem;
  flex-shrink: 0;
  padding-top: 0.15rem;
}

.stack-items {
  font-size: 0.95rem;
}

@media (max-width: 640px) {
  .stack-row { flex-direction: column; gap: 0.3rem; }
  .stack-label { width: auto; }
  .artifact { font-size: 0.72rem; padding: 1.1rem; }
}
</style>
