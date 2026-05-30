<template>
  <section 
    id="characters" 
    class="py-24 px-6 md:px-12 transition-all duration-1000 ease-in-out relative overflow-hidden"
    :style="activeStyle"
  >
    <div class="absolute inset-0 bg-slate-950/60 pointer-events-none"></div>
    <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_70%_50%,transparent_20%,#020408_80%)] pointer-events-none"></div>

    <!-- Floating Particles -->
    <div class="absolute inset-0 pointer-events-none overflow-hidden z-10">
      <div v-for="p in activeParticles" :key="p.id"
        class="absolute rounded-full pointer-events-none"
        :style="{ left: p.x+'%', top: p.y+'%', width: p.size+'px', height: p.size+'px', backgroundColor: activeChar.colorAccent, opacity: p.opacity, boxShadow: `0 0 ${p.size*3}px ${activeChar.colorAccent}`, transform: `translateY(${p.offsetY}px)`, transition: 'all 3s ease' }"
      ></div>
    </div>

    <div class="max-w-7xl mx-auto relative z-20">
      <!-- Section Title -->
      <div class="text-center mb-14 scroll-reveal">
        <span class="font-cinzel text-xs tracking-[0.2em] text-amber-500 uppercase font-semibold">Legendary Figures</span>
        <h2 class="font-herculanum text-4xl md:text-6xl text-gold-gradient tracking-wider mt-2 mb-4">CHARACTER SHOWCASE</h2>
        <div class="w-16 h-[1px] bg-amber-500 mx-auto"></div>
      </div>

      <!-- Main Layout -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 lg:gap-12 items-start">
        
        <!-- Left: Character Info + Thumbnails -->
        <div class="lg:col-span-5 flex flex-col scroll-reveal-left">
          <!-- Nation Tag -->
          <span class="font-cinzel text-xs tracking-[0.2em] uppercase font-bold mb-2 transition-colors duration-500"
            :style="{ color: activeChar.colorAccent }">{{ activeChar.nation }}</span>

          <!-- Name -->
          <h3 class="font-herculanum text-4xl md:text-5xl text-slate-100 tracking-wider mb-3">{{ activeChar.name }}</h3>

          <!-- Bending Badge -->
          <div class="mb-6">
            <span class="px-3 py-1.5 rounded-sm text-[10px] font-cinzel font-bold tracking-widest uppercase transition-colors duration-500"
              :style="{ borderColor: activeChar.colorAccent+'50', backgroundColor: activeChar.colorAccent+'12', color: activeChar.colorAccent, border: '1px solid' }">
              {{ activeChar.bending }}
            </span>
          </div>

          <!-- Lore Card - Glass style -->
          <div class="glass-card rounded-lg p-5 mb-6 relative">
            <p class="font-outfit text-sm text-slate-300 leading-relaxed italic">
              "{{ activeChar.lore }}"
            </p>
          </div>

          <!-- Key Details -->
          <div class="grid grid-cols-2 gap-4 mb-8">
            <div>
              <span class="font-cinzel text-[9px] tracking-widest text-slate-500 uppercase block mb-0.5">Affiliation</span>
              <span class="font-outfit text-sm text-slate-300">{{ activeChar.affiliation }}</span>
            </div>
            <div>
              <span class="font-cinzel text-[9px] tracking-widest text-slate-500 uppercase block mb-0.5">Style</span>
              <span class="font-outfit text-sm text-slate-300">{{ activeChar.style }}</span>
            </div>
          </div>

          <!-- Thumbnail Navigation - MOVED HERE close to content -->
          <div class="border-t border-slate-800/50 pt-5">
            <span class="font-cinzel text-[9px] tracking-widest text-slate-500 uppercase block mb-3">Select Character</span>
            <div class="flex flex-wrap gap-2.5">
              <button
                v-for="(char, index) in characters" :key="char.name"
                @click="selectCharacter(index)"
                :class="[
                  'w-12 h-12 md:w-14 md:h-14 rounded-lg overflow-hidden border-2 transition-all duration-300 focus:outline-none transform hover:-translate-y-0.5 hover:scale-105',
                  activeIndex === index 
                    ? 'scale-110 shadow-lg' : 'border-slate-700/60 grayscale-[70%] hover:grayscale-0 hover:border-slate-500'
                ]"
                :style="activeIndex === index ? { borderColor: activeChar.colorAccent, boxShadow: `0 4px 16px ${activeChar.colorAccent}30` } : {}"
                :aria-label="'Select ' + char.name"
              >
                <img :src="char.image" :alt="char.name" class="w-full h-full object-cover object-top" />
              </button>
            </div>
          </div>
        </div>

        <!-- Right: Character Artwork -->
        <div class="lg:col-span-7 flex justify-center items-center relative min-h-[400px] md:min-h-[520px] scroll-reveal-right">
          <!-- Glow halo -->
          <div class="absolute w-[300px] h-[300px] md:w-[400px] md:h-[400px] rounded-full blur-[80px] opacity-20 transition-all duration-1000"
            :style="{ backgroundColor: activeChar.colorAccent }"></div>
          
          <!-- Decorative ring -->
          <div class="absolute w-[260px] h-[260px] md:w-[360px] md:h-[360px] rounded-full border border-dashed animate-spin-slow pointer-events-none opacity-20 transition-all duration-1000"
            :style="{ borderColor: activeChar.colorAccent+'30' }"></div>

          <!-- Character Image -->
          <transition name="character-fade" mode="out-in">
            <img :key="activeChar.name" :src="activeChar.image" :alt="activeChar.name"
              class="max-h-[360px] md:max-h-[480px] w-auto object-contain relative z-20 filter drop-shadow-[0_8px_24px_rgba(0,0,0,0.85)] select-none hover:scale-[1.03] transition-transform duration-500"
            />
          </transition>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const activeIndex = ref(0)
const particles = ref([])
let particleTimer = null

const activeChar = computed(() => characters[activeIndex.value])
const activeStyle = computed(() => ({
  background: `linear-gradient(135deg, ${activeChar.value.colorDeep} 0%, #030712 100%)`
}))
const activeParticles = computed(() => particles.value)

const selectCharacter = (index) => { activeIndex.value = index; createParticles() }

const createParticles = () => {
  particles.value = Array.from({ length: 14 }, (_, i) => ({
    id: i, x: Math.random()*80+10, y: Math.random()*80+10,
    size: Math.random()*5+3, opacity: Math.random()*0.35+0.08, offsetY: 0
  }))
}

const updateParticles = () => {
  particles.value.forEach(p => {
    p.offsetY -= 0.5; p.x += Math.sin(p.offsetY/25)*0.15
    if (p.offsetY < -160) { p.offsetY = 0; p.x = Math.random()*80+10; p.y = Math.random()*80+10 }
  })
}

onMounted(() => { createParticles(); particleTimer = setInterval(updateParticles, 60) })
onUnmounted(() => clearInterval(particleTimer))

const characters = [
  { name: 'AANG', nation: 'Air Nomads', bending: 'All Elements (Avatar)', affiliation: 'Team Avatar', style: 'Airbending / Glider Staff',
    lore: 'The fun-loving 12-year-old Avatar who was frozen in an iceberg for a century. Aang must balance his childish freedom with the solemn duty of bringing peace to a world torn by the Hundred Year War.',
    image: '/assets/aang.png', colorDeep: '#231e13', colorAccent: '#fbbf24' },
  { name: 'KATARA', nation: 'Water Tribe', bending: 'Waterbending / Healing', affiliation: 'Southern Water Tribe', style: 'Fluid style / Octopus Form',
    lore: 'The last remaining waterbender of the Southern Water Tribe. Driven by compassion and fierce determination, Katara evolves from a self-taught amateur into a powerful master capable of leading nations.',
    image: '/assets/karara-removebg-preview.png', colorDeep: '#08172c', colorAccent: '#38bdf8' },
  { name: 'SOKKA', nation: 'Water Tribe', bending: 'Non-Bender (Warrior)', affiliation: 'Southern Water Tribe', style: 'Space Sword / Boomerang',
    lore: 'A sarcastic, science-loving warrior. Lacking bending powers, Sokka relies on intelligence, tactical planning, and his trusty boomerang to prove his worth in battle.',
    image: '/assets/Sokka__Avatar__The_Last_Airbender_-removebg-preview.png', colorDeep: '#0f172a', colorAccent: '#60a5fa' },
  { name: 'TOPH', nation: 'Earth Kingdom', bending: 'Earthbending / Metalbending', affiliation: 'Beifong Family', style: 'Seismic Sense / Praying Mantis',
    lore: 'The blind, rebellious daughter of the wealthy Beifong family. Toph learned earthbending directly from badgermoles, utilizing seismic vibrations to sense her surroundings and inventing metalbending.',
    image: '/assets/topg.png', colorDeep: '#0c1a10', colorAccent: '#4ade80' },
  { name: 'ZUKO', nation: 'Fire Nation', bending: 'Firebending / Lightning Redir', affiliation: 'Fire Nation Royalty', style: 'Northern Shaolin / Dual Broadswords',
    lore: 'The exiled Prince of the Fire Nation on a desperate quest to capture the Avatar to restore his honor. Zuko undergoes a profound spiritual crisis, realizing his true destiny is to help the Avatar rebuild the world.',
    image: '/assets/zuko.png', colorDeep: '#240606', colorAccent: '#ef4444' },
  { name: 'KORRA', nation: 'Water Tribe', bending: 'All Elements (Avatar)', affiliation: 'Republic City', style: 'Physical Bending / Metalbending',
    lore: 'A headstrong, independent Avatar succeeding Aang. Unlike Aang, Korra is physically gifted and learns the martial aspects of bending easily, but struggles with the spiritual duties of the Avatar.',
    image: '/assets/korra.png', colorDeep: '#061d2d', colorAccent: '#06b6d4' },
  { name: 'ROKU', nation: 'Fire Nation', bending: 'All Elements (Avatar)', affiliation: 'Fire Nation', style: 'Traditional Firebending',
    lore: 'Aang\'s immediate predecessor. Roku was a wise and noble Avatar whose tragic friendship with Fire Lord Sozin inadvertently allowed the War to commence.',
    image: '/assets/roku.png', colorDeep: '#2c0b0b', colorAccent: '#f97316' },
  { name: 'KYOSHI', nation: 'Earth Kingdom', bending: 'All Elements (Avatar)', affiliation: 'Kyoshi Warriors', style: 'Metal War Fans',
    lore: 'The legendary earthborn Avatar who founded Kyoshi Island and the Dai Li. Known for her uncompromising justice, immense physical height, and dual metallic fans.',
    image: '/assets/kyoshi.png', colorDeep: '#131e13', colorAccent: '#a3e635' }
]
</script>

<style scoped>
.character-fade-enter-active { transition: all 0.5s cubic-bezier(0.16,1,0.3,1); }
.character-fade-leave-active { transition: all 0.3s ease; }
.character-fade-enter-from { opacity: 0; transform: scale(0.92) translateX(20px); }
.character-fade-leave-to { opacity: 0; transform: scale(0.96) translateX(-20px); }
</style>
