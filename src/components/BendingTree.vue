<template>
  <section 
    id="bending-tree" 
    class="py-24 px-6 md:px-12 bg-gradient-to-b from-slate-950 via-[#080c18] to-slate-950 relative overflow-hidden"
  >
    <div class="absolute inset-0 bg-[radial-gradient(#1e293b_1px,transparent_1px)] [background-size:24px_24px] opacity-10 pointer-events-none"></div>

    <div class="max-w-7xl mx-auto relative z-10">
      <!-- Section Header -->
      <div class="text-center mb-16 scroll-reveal">
        <h2 class="font-herculanum text-4xl md:text-6xl text-gold-gradient tracking-wider mb-4">
          ELEMENT BENDING TREE
        </h2>
        <p class="font-cinzel text-slate-400 text-xs md:text-sm tracking-widest uppercase max-w-xl mx-auto">
          Click an element to trace its advanced disciplines
        </p>
        <div class="w-24 h-[1px] bg-gradient-to-r from-transparent via-amber-500 to-transparent mx-auto mt-6"></div>
      </div>

      <!-- Root Element Cards - Glass style with BG images -->
      <div class="grid grid-cols-2 lg:grid-cols-4 gap-5 mb-12 scroll-reveal-stagger">
        <button
          v-for="element in elements"
          :key="element.id"
          @click="selectElement(element.id)"
          :class="[
            'relative overflow-hidden rounded-xl text-left transition-all duration-500 transform hover:-translate-y-2 focus:outline-none select-none group h-[220px] md:h-[260px]',
            element.glowClass,
            activeElement === element.id ? 'ring-2 ring-offset-2 ring-offset-slate-950 scale-[1.02] ' + element.ringColor : ''
          ]"
        >
          <!-- Background image -->
          <img :src="element.bgImage" :alt="element.name" class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" />
          
          <!-- Gradient overlay -->
          <div :class="['absolute inset-0 transition-all duration-500', element.overlayGradient]"></div>
          
          <!-- Glass card inner -->
          <div class="absolute inset-0 flex flex-col justify-end p-5 md:p-6 z-10">
            <!-- Element Logo - glows on hover -->
            <div :class="['w-12 h-12 md:w-14 md:h-14 mb-3 flex items-center justify-center transition-all duration-500', element.glowClass]">
              <img :src="element.logoImage" :alt="element.name + ' logo'" :class="['w-full h-full object-contain drop-shadow-lg transition-transform duration-500', element.logoClass]" />
            </div>

            <span :class="['font-cinzel text-[10px] tracking-widest uppercase font-bold mb-1', element.textAccent]">
              {{ element.nation }}
            </span>
            <h3 class="font-herculanum text-2xl md:text-3xl tracking-widest text-white drop-shadow-lg">
              {{ element.name }}
            </h3>
            
            <div class="mt-3 flex items-center gap-2 text-white/50 group-hover:text-white/80 transition-colors">
              <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/></svg>
              <span class="text-[9px] tracking-widest uppercase font-cinzel">
                {{ activeElement === element.id ? 'Collapse' : 'Expand branches' }}
              </span>
            </div>
          </div>
        </button>
      </div>

      <!-- Expanded Branch Container -->
      <transition name="expand">
        <div 
          v-if="activeElementData" 
          class="glass-card rounded-xl p-6 md:p-8 relative overflow-hidden scroll-reveal-scale"
        >
          <!-- Colored glow -->
          <div :class="['absolute -top-32 left-1/2 -translate-x-1/2 w-[400px] h-[400px] rounded-full blur-[120px] pointer-events-none opacity-15 transition-all duration-700', activeElementData.glowBg]"></div>

          <!-- Connection Lines -->
          <div class="hidden md:block w-full h-12 relative mb-4">
            <svg class="w-full h-full absolute top-0 left-0 overflow-visible" viewBox="0 0 800 48">
              <path d="M400,0 L400,16" :class="['stroke-[1.5px] fill-none', activeElementData.strokeColor]"/>
              <path :d="getHorizontalPathD(activeElementData.children.length)" :class="['stroke-[1.5px] fill-none', activeElementData.strokeColor]"/>
              <path 
                v-for="(child, idx) in activeElementData.children" :key="idx"
                :d="getChildPathD(idx, activeElementData.children.length)"
                :class="['stroke-[1.5px] fill-none animate-flow-line', activeElementData.strokeColor]"
              />
            </svg>
          </div>

          <!-- Child Skill Cards - Glass style -->
          <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
            <div
              v-for="child in activeElementData.children"
              :key="child.name"
              @mouseenter="hoveredSkill = child"
              @mouseleave="hoveredSkill = null"
              class="glass-card-light rounded-lg p-5 transition-all duration-300 transform hover:-translate-y-1 hover:shadow-xl select-none group cursor-pointer"
            >
              <div class="flex items-center gap-2.5 mb-3">
                <span :class="['w-2.5 h-2.5 rounded-full shrink-0 transition-shadow duration-300', activeElementData.dotClass, hoveredSkill?.name === child.name ? 'shadow-[0_0_12px_currentColor]' : '']"></span>
                <h4 class="font-cinzel text-sm font-bold tracking-wider text-slate-100 group-hover:text-amber-400 transition-colors">
                  {{ child.name }}
                </h4>
              </div>
              <p class="font-outfit text-xs text-slate-400 leading-relaxed mb-3">
                {{ child.shortSummary }}
              </p>
              <!-- Lore reveal on hover -->
              <transition name="lore-fade">
                <div v-if="hoveredSkill?.name === child.name" class="mt-3 pt-3 border-t border-slate-700/40">
                  <p class="font-outfit text-xs text-amber-200/70 leading-relaxed italic">
                    "{{ child.lore }}"
                  </p>
                </div>
              </transition>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const activeElement = ref('water')
const hoveredSkill = ref(null)

const selectElement = (id) => {
  if (activeElement.value === id) { activeElement.value = null }
  else { activeElement.value = id; hoveredSkill.value = null }
}

const activeElementData = computed(() => elements.find(el => el.id === activeElement.value) || null)

const getHorizontalPathD = (count) => {
  if (count <= 1) return 'M400,16'
  const spacing = 600 / (count - 1)
  const leftX = 400 - (spacing * (count - 1)) / 2
  const rightX = 400 + (spacing * (count - 1)) / 2
  return `M${leftX},16 L${rightX},16`
}
const getChildPathD = (idx, count) => {
  const spacing = 600 / (count - 1 || 1)
  const x = 400 - (spacing * (count - 1)) / 2 + idx * spacing
  return `M${x},16 L${x},48`
}

const elements = [
  {
    id: 'water', name: 'WATER', nation: 'Water Tribe',
    bgImage: '/assets/waterTribe.jpg',
    overlayGradient: 'bg-gradient-to-t from-sky-950/95 via-sky-950/60 to-sky-900/30 group-hover:from-sky-950/90',
    glowClass: 'glow-water',
    ringColor: 'ring-sky-400',
    textAccent: 'text-sky-300',
    glowBg: 'bg-sky-500',
    strokeColor: 'stroke-sky-400/60',
    dotClass: 'bg-sky-400',
    logoImage: '/assets/water.png',
    logoClass: 'scale-[0.85]',
    children: [
      { name: 'Waterbending', shortSummary: 'Fluid movements inspired by moon-drawn tides.', lore: 'Waterbending emphasizes flow, adapting to situations by turning defense into offense. The water bender uses their opponent\'s force against them, channeling energy fluidly.' },
      { name: 'Healing', shortSummary: 'Directing biological energy paths to seal wounds.', lore: 'By utilizing the unique physical and spiritual properties of water, a bender can redirect chi paths within an injured body, accelerating natural recovery.' },
      { name: 'Bloodbending', shortSummary: 'Subjugating fluids inside organic bodies.', lore: 'A dark and terrifying art created by Hama. It allows the bender to take complete control of the blood and muscular systems of living creatures, typically only possible under a full moon.' },
      { name: 'Spiritbending', shortSummary: 'Pacifying or cleansing corrupted spiritual bodies.', lore: 'Developed by Unalaq, this art uses water to surround a spirit, balancing its negative and positive energy to restore order and peace.' }
    ]
  },
  {
    id: 'earth', name: 'EARTH', nation: 'Earth Kingdom',
    bgImage: '/assets/basingse.jpg',
    overlayGradient: 'bg-gradient-to-t from-emerald-950/95 via-emerald-950/60 to-emerald-900/30 group-hover:from-emerald-950/90',
    glowClass: 'glow-earth',
    ringColor: 'ring-emerald-400',
    textAccent: 'text-emerald-300',
    glowBg: 'bg-emerald-500',
    strokeColor: 'stroke-emerald-400/60',
    dotClass: 'bg-emerald-400',
    logoImage: '/assets/earth.png',
    logoClass: 'scale-[0.95]',
    children: [
      { name: 'Earthbending', shortSummary: 'Sturdy stances and direct force manipulation.', lore: 'Earthbending requires a solid connection to the ground. It is defined by patience, direct force, and waiting for the ideal moment to strike with sudden, absolute power.' },
      { name: 'Metalbending', shortSummary: 'Bending the earth impurities left inside metal.', lore: 'Invented by Toph Beifong while locked in a metal cage. By locating the tiny micro-particles of unrefined earth remaining inside forged metals, a master can bend the metal itself.' },
      { name: 'Lavabending', shortSummary: 'Melting stone to command flowing molten magma.', lore: 'An exceedingly rare technique that involves vibrating earth particles rapidly until stone liquifies into lava, enabling control over fluid, thermal magma.' },
      { name: 'Sandbending', shortSummary: 'Controlling loose sand in swirling, shifting forms.', lore: 'Desert nomads developed sandbending to adapt to shifting sands. It requires loose, circular movements, acting almost like a heavy airbending variant.' }
    ]
  },
  {
    id: 'fire', name: 'FIRE', nation: 'Fire Nation',
    bgImage: '/assets/firenation.jpg',
    overlayGradient: 'bg-gradient-to-t from-rose-950/95 via-rose-950/60 to-rose-900/30 group-hover:from-rose-950/90',
    glowClass: 'glow-fire',
    ringColor: 'ring-rose-400',
    textAccent: 'text-rose-300',
    glowBg: 'bg-rose-500',
    strokeColor: 'stroke-rose-400/60',
    dotClass: 'bg-rose-400',
    logoImage: '/assets/fire.png',
    logoClass: 'scale-[1.35]',
    children: [
      { name: 'Firebending', shortSummary: 'Offensive and direct attacks fueled by breath.', lore: 'Firebending is unique because the bender generates the element from their own chi. Fueled by breath and willpower, it is highly aggressive, representing passion and continuous energy.' },
      { name: 'Lightning Generation', shortSummary: 'Separating yin and yang to discharge pure energy.', lore: 'Commonly known as the "cold-blooded fire," this art requires absolute emotional peace. The bender splits positive and negative energies, letting them collide to create lightning.' },
      { name: 'Combustion Bending', shortSummary: 'Projecting mental chi blasts to create explosions.', lore: 'A unique technique that uses a tattoo on the forehead as a focal point to channel telekinetic fire energy, causing massive, long-range explosions.' },
      { name: 'Lightning Redirection', shortSummary: 'Absorbing lightning and redirecting it safely.', lore: 'Created by Iroh after studying waterbending. The bender lets lightning enter one hand, pass through the stomach (sea of chi) without touching the heart, and discharge out the other hand.' }
    ]
  },
  {
    id: 'air', name: 'AIR', nation: 'Air Nomads',
    bgImage: '/assets/airnomadTemple.jpg',
    overlayGradient: 'bg-gradient-to-t from-amber-950/95 via-amber-950/60 to-amber-900/30 group-hover:from-amber-950/90',
    glowClass: 'glow-air',
    ringColor: 'ring-amber-400',
    textAccent: 'text-amber-300',
    glowBg: 'bg-amber-500',
    strokeColor: 'stroke-amber-400/60',
    dotClass: 'bg-amber-400',
    logoImage: '/assets/air.png',
    logoClass: 'scale-[1.4]',
    children: [
      { name: 'Airbending', shortSummary: 'Elusive movements centering on evasion.', lore: 'Airbending is the art of peace and freedom. Benders dodge and weave, finding the path of least resistance. It uses defensive vortexes and rapid agility to disarm foes.' },
      { name: 'Spiritual Projection', shortSummary: 'Projecting soul form out of the physical body.', lore: 'An advanced technique of air monk spirituality. It allows a bender to project their consciousness out of their physical shell, exploring distant places and sensing energy.' },
      { name: 'Flight', shortSummary: 'Letting go of all attachments to float freely.', lore: 'Achieved only by Guru Laghima and Zaheer. By letting go of all earthly attachments ("enter the void, empty and become wind"), a bender releases their connection to gravity to fly.' }
    ]
  }
]
</script>

<style scoped>
.expand-enter-active { transition: all 0.6s cubic-bezier(0.16,1,0.3,1); }
.expand-leave-active { transition: all 0.4s ease; }
.expand-enter-from { opacity: 0; transform: translateY(20px) scale(0.97); }
.expand-leave-to { opacity: 0; transform: translateY(-10px) scale(0.98); }

.lore-fade-enter-active { transition: all 0.4s ease; }
.lore-fade-leave-active { transition: all 0.2s ease; }
.lore-fade-enter-from { opacity: 0; max-height: 0; }
.lore-fade-leave-to { opacity: 0; }
</style>
