<template>
  <section class="relative w-full h-screen flex items-center justify-center overflow-hidden bg-[#0a0a0a]">

    <div class="absolute inset-0 z-0">
      <img src="/images/music-bg.png" class="w-full h-full object-cover will-change-transform" alt="Music Background" />
    </div>

    <div class="absolute inset-0 -z-10 pointer-events-none">
      <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-blue-500/10 blur-[120px] rounded-full animate-pulse"></div>
      <div class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-red-500/10 blur-[120px] rounded-full animate-pulse"
        style="animation-delay: 2s"></div>
    </div>

    <div class="relative z-10 w-full max-w-4xl px-6">

      <div
        class="music-card relative overflow-hidden rounded-[40px] border border-white/10 bg-white/[0.02] p-12 shadow-2xl">

        <div class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center">

          <div class="relative aspect-square rounded-2xl overflow-hidden group">
            <img :src="currentTrack.cover"
              class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" />
            <div class="absolute inset-0 bg-black/20 flex items-center justify-center">
              <svg class="w-32 h-32 -rotate-90">
                <circle cx="64" cy="64" r="60" stroke="white" stroke-width="1" fill="transparent" class="opacity-10" />
                <circle cx="64" cy="64" r="60" stroke="white" stroke-width="2" fill="transparent" stroke-dasharray="377"
                  :stroke-dashoffset="377 - (377 * progress / 100)" class="transition-all duration-300" />
              </svg>
            </div>
          </div>

          <div class="flex flex-col space-y-8">
            <div>
              <h2 class="text-white text-3xl font-serif tracking-widest uppercase mb-2">{{ currentTrack.title }}</h2>
              <p class="text-white/40 text-xs tracking-[0.4em] uppercase">Berlinist • Original Soundtrack</p>
            </div>

            <div class="space-y-2">
              <div class="h-[1px] w-full bg-white/10 relative">
                <div class="absolute h-full bg-white transition-all duration-300" :style="{ width: progress + '%' }">
                </div>
              </div>
              <div class="flex justify-between text-[10px] text-white/30 tracking-widest">
                <span>02:14</span>
                <span>04:30</span>
              </div>
            </div>

            <div class="flex items-center justify-between px-4">
              <button class="text-white/40 hover:text-white transition-colors">
                <span class="material-icons-outlined text-xl">shuffle</span>
              </button>
              <div class="flex items-center gap-8">
                <button class="text-white hover:scale-110 transition-transform">
                  <span class="material-icons text-2xl">skip_previous</span>
                </button>
                <button
                  class="w-16 h-16 rounded-full border border-white/20 flex items-center justify-center hover:bg-white hover:text-black transition-all">
                  <span class="material-icons text-3xl">play_arrow</span>
                </button>
                <button class="text-white hover:scale-110 transition-transform">
                  <span class="material-icons text-2xl">skip_next</span>
                </button>
              </div>
              <button class="text-white/40 hover:text-white transition-colors">
                <span class="material-icons-outlined text-xl">repeat</span>
              </button>
            </div>
          </div>

        </div>

        <div class="mt-12 pt-8 border-t border-white/5">
          <div class="flex gap-6 overflow-x-auto pb-4 no-scrollbar">
            <button v-for="track in tracks" :key="track.id"
              class="flex-shrink-0 text-[10px] tracking-[0.3em] uppercase transition-colors"
              :class="track.id === currentTrack.id ? 'text-white' : 'text-white/20 hover:text-white/50'">
              {{ track.title }}
            </button>
          </div>
        </div>

      </div>

    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';

const progress = ref(45); // Ejemplo de progreso
const tracks = [
  { id: 1, title: 'Gris, Pt. 1', cover: '/images/covers/track1.jpg' },
  { id: 2, title: 'In Your Hands', cover: '/images/covers/track2.jpg' },
  { id: 3, title: 'Unfolding', cover: '/images/covers/track3.jpg' },
  { id: 4, title: 'Debris', cover: '/images/covers/track4.jpg' }
];
const currentTrack = ref(tracks[0]);
</script>

<style scoped>
.music-card {
  /* Fix de performance y visual para el blur */
  backdrop-filter: blur(25px) saturate(150%);
  -webkit-backdrop-filter: blur(25px) saturate(150%);
  will-change: transform;
}

/* Ocultar scrollbar pero mantener funcionalidad */
.no-scrollbar::-webkit-scrollbar {
  display: none;
}

.no-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>
