<template>
  <section 
    id="home" 
    class="relative h-screen w-full flex items-center justify-center overflow-hidden bg-slate-950 z-10"
  >
    <!-- Background Video -->
    <video
      autoplay loop muted playsinline
      class="absolute inset-0 w-full h-full object-cover opacity-55"
      :src="'/assets/sec_hero.mp4'"
    ></video>

    <!-- Cinematic Vignette Overlay -->
    <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-slate-950/30 to-slate-950/60 pointer-events-none"></div>
    <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_center,transparent_20%,#020408_85%)] pointer-events-none"></div>

    <!-- Floating Elemental Glyphs -->
    <div class="absolute inset-0 pointer-events-none z-10 overflow-hidden">
      <div v-for="(glyph, i) in glyphs" :key="i" 
        class="absolute animate-float"
        :class="glyph.class"
        :style="{ animationDelay: glyph.delay, top: glyph.top, left: glyph.left, right: glyph.right }"
      >
        <div :class="['w-14 h-14 md:w-18 md:h-18 flex items-center justify-center', glyph.glow]">
          <img :src="glyph.img" :alt="'Element logo'" :class="['w-full h-full object-contain', glyph.scaleClass]" />
        </div>
      </div>
    </div>
  
    <!-- Content -->
    <div class="relative z-20 max-w-4xl mx-auto px-6 text-center select-none flex flex-col items-center">
      <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full border border-amber-500/25 bg-amber-950/15 mb-8 animate-pulse-soft">
        <span class="w-1.5 h-1.5 rounded-full bg-amber-400 shadow-[0_0_8px_#f59e0b]"></span>
        <span class="font-cinzel text-[10px] md:text-xs tracking-[0.2em] text-amber-400/80 uppercase">
          Interactive Museum Experience
        </span>
      </div>

      <h1 class="font-herculanum text-4xl sm:text-5xl md:text-7xl lg:text-8xl tracking-wider mb-6 text-gold-gradient leading-tight">
        JOURNEY THROUGH THE FOUR NATIONS
      </h1>

      <p class="max-w-2xl text-slate-300/90 font-outfit text-sm sm:text-base md:text-lg leading-relaxed mb-10">
        Discover the cultures, bending arts, legendary Avatars, and the rich history that shaped the world.
      </p>

      <div class="flex flex-col sm:flex-row items-center gap-4">
        <a href="#bending-tree"
          class="px-8 py-3.5 bg-gradient-to-r from-amber-600 to-amber-500 hover:from-amber-500 hover:to-amber-400 text-slate-950 font-cinzel font-bold text-xs tracking-[0.15em] uppercase rounded-sm shadow-xl shadow-amber-900/30 hover:shadow-amber-500/20 transition-all duration-300 hover:-translate-y-0.5 border border-amber-400/30"
        >Start Exploring</a>
        <a href="#world-map"
          class="px-8 py-3.5 bg-slate-950/60 hover:bg-slate-900/80 border border-slate-700/60 hover:border-amber-500/40 text-slate-300 hover:text-amber-400 font-cinzel font-bold text-xs tracking-[0.15em] uppercase rounded-sm transition-all duration-300 hover:-translate-y-0.5 backdrop-blur-sm"
        >View World Map</a>
      </div>

      <!-- Scroll Indicator - Triple Chevron ATLA style -->
      <a 
        href="#bending-tree" 
        @click="hideIndicator"
        :class="[
          'transition-all duration-700 flex flex-col items-center gap-1 group mt-12 md:mt-16 z-30 cursor-pointer select-none',
          isVisible ? 'opacity-100 translate-y-0 pointer-events-auto' : 'opacity-0 -translate-y-4 pointer-events-none'
        ]"
      >
        <span class="font-cinzel text-[9px] tracking-[0.25em] text-amber-500/50 group-hover:text-amber-400 uppercase transition-colors duration-300 mb-1">Explore</span>
        <div class="flex flex-col items-center gap-0">
          <svg class="w-5 h-5 text-amber-500/40 group-hover:text-amber-400 animate-chevron" style="animation-delay: 0s;" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/></svg>
          <svg class="w-5 h-5 text-amber-500/25 group-hover:text-amber-400/70 animate-chevron -mt-2" style="animation-delay: 0.15s;" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/></svg>
          <svg class="w-5 h-5 text-amber-500/15 group-hover:text-amber-400/40 animate-chevron -mt-2" style="animation-delay: 0.3s;" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/></svg>
        </div>
      </a>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const glyphs = [
  { top: '18%', left: '8%', delay: '0s', class: 'opacity-40', glow: 'glow-water',
    img: '/assets/water.png', scaleClass: 'scale-[0.85]' },
  { top: '22%', right: '10%', delay: '1.5s', class: 'opacity-40', glow: 'glow-fire',
    img: '/assets/fire.png', scaleClass: 'scale-[1.35]' },
  { top: '65%', left: '12%', delay: '3s', class: 'opacity-35', glow: 'glow-earth',
    img: '/assets/earth.png', scaleClass: 'scale-[0.95]' },
  { top: '68%', right: '8%', delay: '4.5s', class: 'opacity-35', glow: 'glow-air',
    img: '/assets/air.png', scaleClass: 'scale-[1.4]' },
]


const isVisible = ref(true)

const handleScroll = () => {
  // Only show when the scroll position is at the very top (scrollY < 20)
  isVisible.value = window.scrollY < 20
}

const hideIndicator = () => {
  isVisible.value = false
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

