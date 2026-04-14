<script setup>
import { ref } from 'vue'

// Definimos las piezas de arte y su posición exacta en %
const artPieces = ref([
  { id: 1, x: 25, y: 35, width: 12, src: '/art/square-yellow.webp', blur: true, title: 'Textura 01' },
  { id: 2, x: 65, y: 20, width: 10, src: '/art/square-teal.webp', blur: true, title: 'Textura 02' },
  { id: 3, x: 45, y: 60, width: 15, src: '/art/square-main.webp', blur: false, title: 'Un universo que renace' },
  { id: 4, x: 80, y: 55, width: 14, src: '/art/square-green.webp', blur: true, title: 'Textura 03' },
])
</script>

<template>
  <section class="relative w-full h-screen overflow-hidden bg-black">

    <div class="absolute inset-0 z-0">
      <img
        src="/images/art-bg.png"
        class="w-full h-full object-cover opacity-80"
        alt="Background Forest"
      />
    </div>

    <div class="relative z-10 w-full h-full">

      <div
        v-for="piece in artPieces"
        :key="piece.id"
        class="absolute transform -translate-x-1/2 -translate-y-1/2 transition-all duration-700 hover:scale-110 cursor-pointer group"
        :style="{
          left: piece.x + '%',
          top: piece.y + '%',
          width: piece.width + 'vw'
        }"
      >
        <img
          :src="piece.src"
          :class="[
            'w-full h-auto shadow-2xl transition-all duration-500',
            piece.blur ? 'blur-[8px] group-hover:blur-0 opacity-70 group-hover:opacity-100' : 'opacity-100'
          ]"
        />

        <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity">
           <span class="text-white text-xs tracking-[0.3em] uppercase font-light bg-black/40 px-4 py-2 backdrop-blur-sm">
             {{ piece.title }}
           </span>
        </div>
      </div>

    </div>

    <div class="absolute inset-0 pointer-events-none z-20 flex flex-col justify-center px-[12vw] space-y-4 mt-[11em]">
      <h1 class="text-white text-6xl md:text-6xl font-bold leading-none mix-blend-difference">
        <span class="bg-black/30 px-6 py-3">Un universo<br>que renace</span>
      </h1>
      <p class="text-white text-6xl md:text-6xl font-bold leading-none mix-blend-difference text-right mt-[6rem]">
        en cada textura
      </p>
    </div>

    <div class="absolute bottom-12 left-24 z-20">
      <p class="text-white/70 text-sm tracking-[0.1em] uppercase font-medium">
        Descubre los secretos que guardan los árboles
      </p>
    </div>
  </section>
</template>

<style scoped>
/* Animación de flotación suave para las piezas */
.absolute.group {
  animation: float 6s ease-in-out infinite;
}

@keyframes float {
  0%, 100% { transform: translate(-50%, -52%); }
  50% { transform: translate(-50%, -48%); }
}

/* Retraso aleatorio para que no se muevan todas iguales */
.absolute.group:nth-child(even) {
  animation-duration: 8s;
  animation-delay: 1s;
}
</style>
