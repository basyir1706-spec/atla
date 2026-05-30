<template>
  <div>
    <!-- ======== INTERACTIVE MAP ======== -->
    <section id="world-map" class="py-24 px-6 md:px-12 bg-slate-950 relative overflow-hidden">
      <div class="max-w-7xl mx-auto">
        <div class="text-center mb-14 scroll-reveal">
          <span class="font-cinzel text-xs tracking-[0.2em] text-amber-500 uppercase font-semibold">Cartography</span>
          <h2 class="font-herculanum text-4xl md:text-6xl text-gold-gradient tracking-wider mt-2 mb-4">EXPLORE THE WORLD</h2>
          <p class="font-outfit text-sm text-slate-400 max-w-lg mx-auto">Hover over the regions to identify the four sovereign territories. Scroll below to discover each nation.</p>
          <div class="w-16 h-[1px] bg-amber-500 mx-auto mt-6"></div>
        </div>

        <!-- Map Container -->
        <div class="glass-card p-3 md:p-6 rounded-xl mb-4 scroll-reveal-scale">
          <div class="w-full flex justify-center items-center select-none">
            <img src="/assets/map.jpg" alt="World Map of the Four Nations" class="w-full max-w-[900px] h-auto rounded-lg shadow-lg" />
          </div>
        </div>
      </div>
    </section>

    <!-- ======== WATER TRIBE SECTION ======== -->
    <section id="nation-water" class="relative min-h-[80vh] overflow-hidden">
      <div class="nation-hero absolute inset-0" style="background-image: url('/assets/waterTribe.jpg')"></div>
      <div class="absolute inset-0 bg-gradient-to-r from-sky-950/95 via-sky-950/80 to-sky-950/50"></div>
      <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-transparent to-slate-950/40"></div>
      <div class="relative z-10 max-w-7xl mx-auto px-6 md:px-12 py-24 grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <div class="scroll-reveal-left">
          <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 flex items-center justify-center glow-water">
              <img src="/assets/water.png" alt="Water Tribe logo" class="w-full h-full object-contain scale-[0.85]" />
            </div>
            <span class="font-cinzel text-xs tracking-[0.2em] text-sky-400 uppercase font-bold">Sovereign Territory</span>
          </div>
          <h3 class="font-herculanum text-4xl md:text-6xl text-white tracking-wider mb-6">WATER TRIBE</h3>
          <div class="space-y-5">
            <div><strong class="font-cinzel text-sky-400/80 text-[10px] tracking-widest uppercase block mb-1">Culture & Values</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Centered on family, community, and adaptation. The tribes maintain a deep connection to the Moon and Ocean spirits, learning that strength lies in working together like water flowing in unison.</p></div>
            <div><strong class="font-cinzel text-sky-400/80 text-[10px] tracking-widest uppercase block mb-1">Lifestyle</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Living in the frozen polar landscapes, they are hunters, navigators, and craftsmen. They rely on waterbending for defense, construction, navigation, and healing.</p></div>
            <div><strong class="font-cinzel text-sky-400/80 text-[10px] tracking-widest uppercase block mb-1">Architecture</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Magnificent palaces and aqueducts crafted entirely of ice. Glacial caves, skin-canoes, polar landscapes inhabited by polar bear-dogs.</p></div>
          </div>
        </div>
        <div class="scroll-reveal-right flex justify-center">
          <div class="relative w-full max-w-md rounded-xl overflow-hidden border border-sky-500/20 shadow-2xl shadow-sky-950/50">
            <img src="/assets/waterTribe.jpg" alt="Water Tribe" class="w-full h-[350px] object-cover"/>
            <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-sky-950 p-4">
              <span class="font-cinzel text-sky-300 text-xs tracking-widest uppercase">Capital: Agna Qel'a</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ======== EARTH KINGDOM SECTION ======== -->
    <section id="nation-earth" class="relative min-h-[80vh] overflow-hidden">
      <div class="nation-hero absolute inset-0" style="background-image: url('/assets/basingse.jpg')"></div>
      <div class="absolute inset-0 bg-gradient-to-l from-emerald-950/95 via-emerald-950/80 to-emerald-950/50"></div>
      <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-transparent to-slate-950/40"></div>
      <div class="relative z-10 max-w-7xl mx-auto px-6 md:px-12 py-24 grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <div class="order-2 lg:order-1 scroll-reveal-left flex justify-center">
          <div class="relative w-full max-w-md rounded-xl overflow-hidden border border-emerald-500/20 shadow-2xl shadow-emerald-950/50">
            <img src="/assets/basingse.jpg" alt="Ba Sing Se" class="w-full h-[350px] object-cover"/>
            <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-emerald-950 p-4">
              <span class="font-cinzel text-emerald-300 text-xs tracking-widest uppercase">Capital: Ba Sing Se</span>
            </div>
          </div>
        </div>
        <div class="order-1 lg:order-2 scroll-reveal-right">
          <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 flex items-center justify-center glow-earth">
              <img src="/assets/earth.png" alt="Earth Kingdom logo" class="w-full h-full object-contain scale-[0.95]" />
            </div>
            <span class="font-cinzel text-xs tracking-[0.2em] text-emerald-400 uppercase font-bold">Sovereign Territory</span>
          </div>
          <h3 class="font-herculanum text-4xl md:text-6xl text-white tracking-wider mb-6">EARTH KINGDOM</h3>
          <div class="space-y-5">
            <div><strong class="font-cinzel text-emerald-400/80 text-[10px] tracking-widest uppercase block mb-1">Culture & Values</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Values resilience, fortitude, and tradition. They are proud, hardworking, and strong-willed. Reflecting the rock they bend, they endure struggles with patient strength.</p></div>
            <div><strong class="font-cinzel text-emerald-400/80 text-[10px] tracking-widest uppercase block mb-1">Lifestyle</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">A vast and diverse continent spanning rural villages, bustling desert networks, and enormous walled cities. Lifestyles vary from agricultural farming to industrial districts.</p></div>
            <div><strong class="font-cinzel text-emerald-400/80 text-[10px] tracking-widest uppercase block mb-1">Architecture</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Enormous stone walls of Ba Sing Se, architectural structures decorated with gold-lacquered rings, green ceramic roofs, and vast forests, mountains, and plains.</p></div>
          </div>
        </div>
      </div>
    </section>

    <!-- ======== FIRE NATION SECTION ======== -->
    <section id="nation-fire" class="relative min-h-[80vh] overflow-hidden">
      <div class="nation-hero absolute inset-0" style="background-image: url('/assets/firenation.jpg')"></div>
      <div class="absolute inset-0 bg-gradient-to-r from-rose-950/95 via-rose-950/80 to-rose-950/50"></div>
      <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-transparent to-slate-950/40"></div>
      <div class="relative z-10 max-w-7xl mx-auto px-6 md:px-12 py-24 grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <div class="scroll-reveal-left">
          <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 flex items-center justify-center glow-fire">
              <img src="/assets/fire.png" alt="Fire Nation logo" class="w-full h-full object-contain scale-[1.35]" />
            </div>
            <span class="font-cinzel text-xs tracking-[0.2em] text-rose-400 uppercase font-bold">Sovereign Territory</span>
          </div>
          <h3 class="font-herculanum text-4xl md:text-6xl text-white tracking-wider mb-6">FIRE NATION</h3>
          <div class="space-y-5">
            <div><strong class="font-cinzel text-rose-400/80 text-[10px] tracking-widest uppercase block mb-1">Culture & Values</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Driven by energy, passion, ambition, and progress. They value honor, respect, and technological innovation. Historically structured around military prowess.</p></div>
            <div><strong class="font-cinzel text-rose-400/80 text-[10px] tracking-widest uppercase block mb-1">Lifestyle</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Highly industrialized volcanic islands. Citizens engage in coal mining, steel metallurgy, naval shipbuilding, and martial arts military schools.</p></div>
            <div><strong class="font-cinzel text-rose-400/80 text-[10px] tracking-widest uppercase block mb-1">Architecture</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Volcanic mountains, pagodas with curved red-tile roofs, massive metal warships, lava-powered industrial factories, and royal halls lined with burning oil cauldrons.</p></div>
          </div>
        </div>
        <div class="scroll-reveal-right flex justify-center">
          <div class="relative w-full max-w-md rounded-xl overflow-hidden border border-rose-500/20 shadow-2xl shadow-rose-950/50">
            <img src="/assets/firenation.jpg" alt="Fire Nation" class="w-full h-[350px] object-cover"/>
            <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-rose-950 p-4">
              <span class="font-cinzel text-rose-300 text-xs tracking-widest uppercase">Capital: Caldera City</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ======== AIR NOMADS SECTION ======== -->
    <section id="nation-air" class="relative min-h-[80vh] overflow-hidden">
      <div class="nation-hero absolute inset-0" style="background-image: url('/assets/airnomadTemple.jpg')"></div>
      <div class="absolute inset-0 bg-gradient-to-l from-amber-950/95 via-amber-950/80 to-amber-950/50"></div>
      <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-transparent to-slate-950/40"></div>
      <div class="relative z-10 max-w-7xl mx-auto px-6 md:px-12 py-24 grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <div class="order-2 lg:order-1 scroll-reveal-left flex justify-center">
          <div class="relative w-full max-w-md rounded-xl overflow-hidden border border-amber-500/20 shadow-2xl shadow-amber-950/50">
            <img src="/assets/airnomadTemple.jpg" alt="Air Nomad Temple" class="w-full h-[350px] object-cover"/>
            <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-amber-950 p-4">
              <span class="font-cinzel text-amber-300 text-xs tracking-widest uppercase">Southern Air Temple</span>
            </div>
          </div>
        </div>
        <div class="order-1 lg:order-2 scroll-reveal-right">
          <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 flex items-center justify-center glow-air">
              <img src="/assets/air.png" alt="Air Nomads logo" class="w-full h-full object-contain scale-[1.4]" />
            </div>
            <span class="font-cinzel text-xs tracking-[0.2em] text-amber-400 uppercase font-bold">Sovereign Territory</span>
          </div>
          <h3 class="font-herculanum text-4xl md:text-6xl text-white tracking-wider mb-6">AIR NOMADS</h3>
          <div class="space-y-5">
            <div><strong class="font-cinzel text-amber-400/80 text-[10px] tracking-widest uppercase block mb-1">Culture & Spirituality</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Deeply spiritual, peaceful, and detached from worldly desires. They value freedom, meditation, and harmony with nature. 100% of their population was born with airbending.</p></div>
            <div><strong class="font-cinzel text-amber-400/80 text-[10px] tracking-widest uppercase block mb-1">Lifestyle</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">Monastic communities of monks and nuns who are vegetarian and live in high, isolated mountain peaks. They travel on flying bison and practice meditation.</p></div>
            <div><strong class="font-cinzel text-amber-400/80 text-[10px] tracking-widest uppercase block mb-1">Architecture</strong>
              <p class="font-outfit text-sm text-slate-300 leading-relaxed">White stone temples on mountain cliffs, spinning wind turbines, floating structures, hanging gardens, and monks in cream-orange robes alongside sky bison.</p></div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const hovered = ref('')
</script>
