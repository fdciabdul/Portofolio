<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'
import CvPage from './components/CvPage.vue'
import ProjectsDoc from './components/ProjectsDoc.vue'

const route = ref(window.location.hash)

function onHashChange() {
  route.value = window.location.hash
  window.scrollTo(0, 0)
}

onMounted(() => window.addEventListener('hashchange', onHashChange))
onUnmounted(() => window.removeEventListener('hashchange', onHashChange))
</script>

<template>
  <CvPage v-if="route.startsWith('#/cv')" />
  <ProjectsDoc v-else-if="route.startsWith('#/projects-pdf')" />

  <template v-else>
    <NavBar />
    <main>
      <HeroSection />
      <ProjectsSection />
      <AboutSection />
      <ContactSection />
    </main>
    <FooterSection />
  </template>
</template>

<style>
main > section:first-child {
  padding-top: 2rem;
}
</style>
