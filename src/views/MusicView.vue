<template>
  <section class="relative w-full h-screen overflow-hidden bg-black flex items-center justify-center">

    <div class="absolute inset-0 z-0">
      <img src="/images/music-bg.png" alt="Arte Detallado del Bosque y Cascada (Gris)"
        class="w-full h-full object-cover transition-transform duration-600 will-change-transform" />
    </div>

    <div class="absolute inset-0 flex items-center justify-center z-10">
      <div class="text-center translate-y-12">
        <p
          class="text-white text-6xl md:text-7xl font-sans font-bold leading-none tracking-tighter uppercase mb-6 opacity-60">
          sonoro
        </p>
      </div>
    </div>

    <div class="absolute inset-0 z-20 overflow-hidden pointer-events-none">
      <img src="/images/music-bg2.png"
        class="w-full h-full object-cover transition-transform duration-600 will-change-transform" id="parallax-bg-2" />
    </div>

    <div class="absolute top-24 left-16 z-20">
      <p class="text-white/70 text-sm tracking-[0.1em] uppercase font-medium">
        Pasa el cursor por las cascadas para crear melodías
      </p>
    </div>

    <div class="absolute inset-0 flex items-center justify-center z-30 pointer-events-none">
      <div class="text-center">
        <p class="text-white text-6xl md:text-7xl font-sans font-bold leading-none tracking-tighter uppercase mb-6">
          Un paisaje
        </p>
      </div>
    </div>

    <div class="absolute bottom-16 left-1/2 -translate-x-1/2 z-20">
      <a href="https://open.spotify.com/album/2YMWspDGtbDgYULXvVQFM6" target="_blank"
        class="inline-flex items-center gap-4 bg-white/70 backdrop-blur-md px-10 py-3 rounded-full border border-white/20 transition-all duration-300 hover:bg-[#1DB954] hover:scale-105 shadow-xl group">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="white" xmlns="http://www.w3.org/1999/xlink"
          class="fill-black group-hover:fill-white transition-colors">
          <path
            d="M12,0C5.37,0,0,5.37,0,12c0,6.63,5.37,12,12,12c6.63,0,12-5.37,12-12C24,5.37,18.63,0,12,0z M17.48,17.29c-0.22,0.36-0.69,0.48-1.06,0.26 c-2.83-1.73-6.39-2.13-10.59-1.17c-0.42,0.1-0.84-0.16-0.93-0.58C4.81,15.39,5.07,14.97,5.49,14.88c4.61-1.06,8.54-0.61,11.73,1.35 C17.59,16.45,17.71,16.92,17.48,17.29z M18.91,14.16c-0.28,0.46-0.88,0.61-1.34,0.33c-3.23-1.99-8.17-2.58-12-1.42 c-0.53,0.16-1.08-0.14-1.24-0.67c-0.16-0.53,0.14-1.08,0.67-1.24c4.37-1.33,9.81-0.66,13.59,1.66 C19.06,13.08,19.21,13.68,18.91,14.16z M19.04,11.16C15.18,8.87,8.79,8.65,5.1,9.76c-0.59,0.18-1.22-0.15-1.4-0.74 c-0.18-0.59,0.15-1.22,0.74-1.4c4.27-1.29,11.33-1.04,15.77,1.59c0.53,0.32,0.7,1.01,0.38,1.55 C19.86,11.05,19.17,11.23,19.04,11.16z" />
        </svg>
        <span
          class="text-black tracking-wide uppercase text-sm font-semibold whitespace-nowrap group-hover:text-white transition-colors">
          BANDA SONORA OFICIAL
        </span>
      </a>
    </div>

    <svg viewBox="0 0 100 100" preserveAspectRatio="none"
      class="absolute inset-0 z-40 w-full h-full pointer-events-none">
      <g v-for="i in 8" :key="'waterfall-' + i">
        <line :x1="25 + i * 5" y1="0" :x2="25 + i * 5" y2="100" stroke="white" stroke-width="2"
          class="waterfall-line opacity-0 transition-opacity duration-300 cursor-pointer pointer-events-auto"
          @mouseenter="playHarmonic(i)" />
        <line :x1="25 + i * 5" y1="20" :x2="25 + i * 5" y2="80" stroke="white" stroke-width="0.5"
          class="waterfall-line-core opacity-0 pointer-events-none" :id="'line-core-' + i" />
      </g>
      <g class="cursor-trails z-10">
        <circle cx="45" cy="40" r="0.5" fill="white" class="opacity-10" />
        <circle cx="55" cy="45" r="0.8" fill="white" class="opacity-15" />
        <circle cx="50" cy="35" r="0.5" fill="white" class="opacity-10" />
      </g>
    </svg>

  </section>
</template>

<script setup>
import { onMounted } from 'vue';
import gsap from 'gsap';

const notes = [
  261.63, // C4 (Do)
  293.66, // D4 (Re)
  329.63, // E4 (Mi)
  349.23, // F4 (Fa)
  392.00, // G4 (Sol)
  440.00, // A4 (La)
  493.88, // B4 (Si)
  523.25  // C5 (Do octava)
];

const playHarmonic = (index) => {
  // 1. Animación Visual (GSAP)
  gsap.fromTo(`#line-core-${index}`,
    { opacity: 0.8, scaleY: 0 },
    { opacity: 0, scaleY: 1.5, duration: 2, ease: "power2.out" }
  );

  // 2. Síntesis de Audio
  const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  const oscillator = audioCtx.createOscillator();
  const gainNode = audioCtx.createGain();

  // Configuración del timbre (Onda Senoidal = Suave/Celestial)
  oscillator.type = 'sine';
  oscillator.frequency.setValueAtTime(notes[index - 1], audioCtx.currentTime);

  // Envolvente de volumen (Para que no suene como un pitido seco)
  gainNode.gain.setValueAtTime(0, audioCtx.currentTime);
  // Ataque rápido pero no instantáneo (evita "clicks")
  gainNode.gain.linearRampToValueAtTime(0.15, audioCtx.currentTime + 0.1);
  // Caída larga (Efecto de campana/reverberación)
  gainNode.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + 2.0);

  oscillator.connect(gainNode);
  gainNode.connect(audioCtx.destination);

  oscillator.start();
  oscillator.stop(audioCtx.currentTime + 2.0);
};
</script>

<style scoped>
/* Hacemos que las líneas vibren un poco al tocarlas */
.waterfall-line:hover {
  filter: url(#waterfall-glow);
  stroke-width: 4;
}

/* Animación de las partículas (cursor-trails) */
.cursor-trails circle {
  animation: float 4s infinite ease-in-out;
}

@keyframes float {

  0%,
  100% {
    transform: translateY(0);
    opacity: 0.1;
  }

  50% {
    transform: translateY(-20px);
    opacity: 0.3;
  }
}
</style>
