<template>
  <nav
    :class="[
      'fixed top-0 left-0 right-0 z-50 transition-all duration-500 ease-out border-b px-6 md:px-12',
      isScrolled 
        ? 'py-3 bg-slate-950/85 backdrop-blur-md border-slate-800/80 shadow-lg shadow-black/40' 
        : 'py-6 bg-transparent border-transparent'
    ]"
  >
    <div class="max-w-7xl mx-auto flex items-center justify-between">
      <!-- Logo -->
      <a href="#home" class="flex items-center gap-3 group focus:outline-none">
        <img 
          src="/assets/logo.png" 
          alt="Avatar Logo" 
          :class="['transition-all duration-500 select-none', isScrolled ? 'h-8 md:h-9' : 'h-10 md:h-12']"
        />
        <span class="hidden sm:inline-block font-cinzel text-xs text-amber-500/80 tracking-widest uppercase border-l border-amber-500/30 pl-3">
          Chronicles
        </span>
      </a>

      <!-- Desktop Links -->
      <div class="hidden lg:flex items-center gap-8">
        <a 
          v-for="link in navLinks" 
          :key="link.name" 
          :href="link.href"
          class="font-cinzel text-sm text-slate-300 hover:text-amber-400 tracking-wider transition-colors duration-300 uppercase relative py-1 after:content-[''] after:absolute after:bottom-0 after:left-0 after:w-0 after:h-[1px] after:bg-amber-400 after:transition-all after:duration-300 hover:after:w-full"
        >
          {{ link.name }}
        </a>
      </div>

      <!-- Right Action Button -->
      <div class="hidden sm:flex items-center">
        <a
          href="#world-map"
          class="px-5 py-2.5 bg-gradient-to-r from-amber-600 to-amber-500 hover:from-amber-500 hover:to-amber-400 text-slate-950 font-cinzel font-semibold text-xs tracking-widest uppercase rounded shadow-lg shadow-amber-950/50 hover:shadow-amber-500/25 transition-all duration-300 transform hover:-translate-y-0.5 border border-amber-400/40"
        >
          Explore World
        </a>
      </div>

      <!-- Mobile Menu Button -->
      <button 
        @click="isMobileMenuOpen = !isMobileMenuOpen"
        class="lg:hidden p-2 text-slate-400 hover:text-amber-400 focus:outline-none transition-colors duration-300"
        aria-label="Toggle menu"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path v-if="isMobileMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>
    </div>

    <!-- Mobile Drawer -->
    <transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="transform -translate-y-full opacity-0"
      enter-to-class="transform translate-y-0 opacity-100"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="transform translate-y-0 opacity-100"
      leave-to-class="transform -translate-y-full opacity-0"
    >
      <div v-if="isMobileMenuOpen" class="lg:hidden absolute top-full left-0 right-0 bg-slate-950/95 border-b border-slate-800/80 px-6 py-8 flex flex-col gap-6 shadow-2xl backdrop-blur-lg">
        <a 
          v-for="link in navLinks" 
          :key="link.name" 
          :href="link.href"
          @click="isMobileMenuOpen = false"
          class="font-cinzel text-lg text-slate-300 hover:text-amber-400 tracking-wider transition-colors duration-300 uppercase py-2 border-b border-slate-900"
        >
          {{ link.name }}
        </a>
        <a
          href="#world-map"
          @click="isMobileMenuOpen = false"
          class="w-full text-center py-3 bg-gradient-to-r from-amber-600 to-amber-500 text-slate-950 font-cinzel font-semibold text-sm tracking-widest uppercase rounded shadow-lg shadow-amber-950/30 transition-all duration-300"
        >
          Explore World
        </a>
      </div>
    </transition>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const navLinks = [
  { name: 'Home', href: '#home' },
  { name: 'Elements', href: '#bending-tree' },
  { name: 'Characters', href: '#characters' },
  { name: 'World Map', href: '#world-map' },
  { name: 'Nations', href: '#nation-water' },
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 40
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  // Check initial state in case of page reload halfway down
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>
