<template>
  <div class="min-h-screen bg-slate-950 text-slate-100 flex flex-col font-outfit">
    <FloatingNavbar />
    <main class="flex-grow">
      <HeroSection />
      <BendingTree />
      <CharacterCarousel />
      <WorldMap />
    </main>
    <MainFooter />
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import FloatingNavbar from './components/FloatingNavbar.vue'
import HeroSection from './components/HeroSection.vue'
import BendingTree from './components/BendingTree.vue'
import CharacterCarousel from './components/CharacterCarousel.vue'
import WorldMap from './components/WorldMap.vue'
import MainFooter from './components/MainFooter.vue'

onMounted(() => {
  // Scroll-reveal animation system using IntersectionObserver
  const revealClasses = [
    'scroll-reveal', 'scroll-reveal-left', 'scroll-reveal-right',
    'scroll-reveal-scale', 'scroll-reveal-stagger'
  ]

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('revealed')
      }
    })
  }, { threshold: 0.08, rootMargin: '0px 0px -40px 0px' })

  // Observe all elements with reveal classes
  revealClasses.forEach(cls => {
    document.querySelectorAll(`.${cls}`).forEach(el => observer.observe(el))
  })

  // Re-observe when new content is dynamically added (e.g. Vue transitions)
  const mutationObserver = new MutationObserver(() => {
    revealClasses.forEach(cls => {
      document.querySelectorAll(`.${cls}:not(.revealed)`).forEach(el => observer.observe(el))
    })
  })
  mutationObserver.observe(document.body, { childList: true, subtree: true })
})
</script>

<style>
body { margin: 0; padding: 0; background-color: #020408; }
</style>
