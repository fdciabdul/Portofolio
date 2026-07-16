<script setup lang="ts">
const year = new Date().getFullYear()
</script>

<template>
  <footer class="footer">
    <div class="container footer-inner">
      <span>© {{ year }} Abdul Muttaqin</span>
      <span class="footer-note">Built with Vue. Hosted on GitHub Pages.</span>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  border-top: 1px solid var(--rule);
  padding: 2.5rem 0 3.5rem;
}

.footer-inner {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  font-family: var(--mono);
  font-size: 0.72rem;
  color: var(--muted);
}

@media (max-width: 560px) {
  .footer-inner { flex-direction: column; gap: 0.4rem; }
}
</style>
