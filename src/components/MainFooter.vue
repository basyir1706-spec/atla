<template>
  <footer 
    id="about" 
    class="bg-slate-950 text-slate-400 border-t border-slate-900 pt-20 pb-10 px-6 md:px-12 relative overflow-hidden"
  >
    <!-- Background Watermark Symbol -->
    <div class="absolute -right-24 -bottom-24 w-80 h-80 text-slate-900 pointer-events-none opacity-20">
      <svg viewBox="0 0 100 100" fill="currentColor">
        <path d="M50,15 C50,15 65,30 65,55 C65,70 55,80 50,80 C45,80 35,70 35,55 C35,30 50,15 Z M50,40 C52,48 58,54 58,62 C58,68 54,72 50,72"/>
      </svg>
    </div>

    <div class="max-w-7xl mx-auto relative z-10">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-12 gap-12 pb-16 border-b border-slate-900">
        <!-- Col 1: About (5 Cols) -->
        <div class="lg:col-span-5 text-left flex flex-col justify-between">
          <div>
            <h3 class="font-herculanum text-2xl text-gold-gradient tracking-widest mb-4">
              AVATAR CHRONICLES
            </h3>
            <p class="font-outfit text-sm text-slate-400 leading-relaxed max-w-sm">
              An immersive digital museum and tribute to the rich history, bending disciplines, legendary characters, and diverse nations of Avatar: The Last Airbender.
            </p>
          </div>
          
          <!-- Social Links -->
          <div class="mt-8 flex items-center gap-4">
            <a 
              v-for="social in socials" 
              :key="social.name" 
              :href="social.link"
              target="_blank"
              class="w-10 h-10 rounded-full border border-slate-800 bg-slate-950 flex items-center justify-center hover:border-amber-500 hover:text-amber-400 transition-all duration-300 transform hover:-translate-y-1 shadow-md shadow-black/50"
              :aria-label="social.name"
            >
              <component :is="social.icon" class="w-4.5 h-4.5" />
            </a>
          </div>
        </div>

        <!-- Col 2: Quick Links (3 Cols) -->
        <div class="lg:col-span-3 text-left">
          <h4 class="font-cinzel text-xs tracking-widest text-slate-300 font-bold uppercase mb-6">
            Quick Navigation
          </h4>
          <ul class="space-y-3 font-outfit text-sm">
            <li v-for="link in navLinks" :key="link.name">
              <a 
                :href="link.href" 
                class="hover:text-amber-400 transition-colors duration-300 flex items-center gap-1.5"
              >
                <span class="text-[8px] text-amber-500">•</span>
                {{ link.name }}
              </a>
            </li>
          </ul>
        </div>

        <!-- Col 3: Contact & Info (4 Cols) -->
        <div class="lg:col-span-4 text-left">
          <h4 class="font-cinzel text-xs tracking-widest text-slate-300 font-bold uppercase mb-6">
            Keep in Touch
          </h4>
          <p class="font-outfit text-sm text-slate-400 mb-4 leading-relaxed">
            Have feedback or want to collaborate on expanding the Chronicles? Reach out to our team of dedicated fans.
          </p>
          <div class="space-y-2 text-sm font-outfit">
            <p class="flex items-center gap-2">
              <span class="font-cinzel text-xs text-amber-500/80 uppercase font-semibold">Email:</span>
              <a href="mailto:explorer@avatar-chronicles.net" class="hover:text-amber-400 transition-colors text-slate-300">
                explorer@avatar-chronicles.net
              </a>
            </p>
            <p class="flex items-center gap-2">
              <span class="font-cinzel text-xs text-amber-500/80 uppercase font-semibold">Location:</span>
              <span class="text-slate-300">Four Nations Cultural Center</span>
            </p>
          </div>
        </div>
      </div>

      <!-- Credits and Disclaimer -->
      <div class="pt-8 flex flex-col md:flex-row items-center justify-between gap-6 text-xs text-slate-600 font-outfit select-none">
        <p class="text-center md:text-left">
          &copy; 2026 Avatar Chronicles. Designed & developed with Vue 3 and Tailwind CSS.
        </p>
        <p class="max-w-md text-center md:text-right leading-relaxed italic border-l-0 md:border-l md:border-slate-900 md:pl-6">
          This website is a non-commercial, fan-made tribute project. All Avatar: The Last Airbender characters, artwork, and elements are trademarked by Nickelodeon and Viacom Media Networks.
        </p>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { h } from 'vue'

const navLinks = [
  { name: 'Home Base', href: '#home' },
  { name: 'Bending Tree', href: '#bending-tree' },
  { name: 'Character Carousel', href: '#characters' },
  { name: 'Four Territories', href: '#world-map' },
  { name: 'World Map', href: '#world-map' }
]

// Custom Lucide-like SVG renders for social links
const socials = [
  {
    name: 'Instagram',
    link: 'https://instagram.com',
    icon: {
      render: () => h('svg', {
        xmlns: 'http://www.w3.org/2000/svg',
        viewBox: '0 0 24 24',
        fill: 'none',
        stroke: 'currentColor',
        'stroke-width': '2',
        'stroke-linecap': 'round',
        'stroke-linejoin': 'round',
      }, [
        h('rect', { x: '2', y: '2', width: '20', height: '20', rx: '5', ry: '5' }),
        h('path', { d: 'M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z' }),
        h('line', { x1: '17.5', y1: '6.5', x2: '17.51', y2: '6.5' }),
      ])
    }
  },
  {
    name: 'X',
    link: 'https://x.com',
    icon: {
      render: () => h('svg', {
        xmlns: 'http://www.w3.org/2000/svg',
        viewBox: '0 0 24 24',
        fill: 'none',
        stroke: 'currentColor',
        'stroke-width': '2',
        'stroke-linecap': 'round',
        'stroke-linejoin': 'round',
      }, [
        h('path', { d: 'M4 4l11.733 16h4.267l-11.733 -16z' }),
        h('path', { d: 'M4 20l6.768 -6.768m2.46 -2.46l6.772 -6.772' }),
      ])
    }
  },
  {
    name: 'Facebook',
    link: 'https://facebook.com',
    icon: {
      render: () => h('svg', {
        xmlns: 'http://www.w3.org/2000/svg',
        viewBox: '0 0 24 24',
        fill: 'none',
        stroke: 'currentColor',
        'stroke-width': '2',
        'stroke-linecap': 'round',
        'stroke-linejoin': 'round',
      }, [
        h('path', { d: 'M18 2h-3a5 5 0 0 0 -5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z' }),
      ])
    }
  },
  {
    name: 'YouTube',
    link: 'https://youtube.com',
    icon: {
      render: () => h('svg', {
        xmlns: 'http://www.w3.org/2000/svg',
        viewBox: '0 0 24 24',
        fill: 'none',
        stroke: 'currentColor',
        'stroke-width': '2',
        'stroke-linecap': 'round',
        'stroke-linejoin': 'round',
      }, [
        h('path', { d: 'M22.54 6.42a2.78 2.78 0 0 0 -1.95 -1.96C18.88 4 12 4 12 4s-6.88 0 -8.59.46a2.78 2.78 0 0 0 -1.95 1.96A29 29 0 0 0 1 12a29 29 0 0 0 .46 5.58 2.78 2.78 0 0 0 1.95 1.96C5.12 20 12 20 12 20s6.88 0 8.59-.46a2.78 2.78 0 0 0 1.95 -1.96A29 29 0 0 0 23 12a29 29 0 0 0 -.46 -5.58z' }),
        h('polygon', { points: '9.75,15.02 15.5,12 9.75,8.98', fill: 'currentColor' }),
      ])
    }
  }
]
</script>
