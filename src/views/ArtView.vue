<script setup>
import { ref } from 'vue'
import { pieces } from '@/data/artpieces';

const artPieces = ref(pieces)
const activeNode = ref(null);

const selectNode = (node) => {
  activeNode.value = node;
};
</script>

<template>
  <section class="relative w-full h-screen overflow-hidden bg-black">

    <div class="absolute inset-0 z-0">
      <img src="/images/art-bg.png" class="w-full h-full object-cover" alt="Background Forest" />
    </div>

    <div class="relative z-10 w-full h-full">

      <div v-for="piece in artPieces" :key="piece.id"
        class="absolute transform -translate-x-1/2 -translate-y-1/2 transition-all duration-700 hover:scale-105 cursor-pointer group"
        :style="{
          left: piece.x + '%',
          top: piece.y + '%',
          width: piece.width + 'vw'
        }">
        <img  @click="selectNode(piece)" :src="piece.src" :class="[
          'w-full h-auto shadow-2xl transition-all duration-500',
          piece.blur ? 'blur-[8px] group-hover:blur-0 opacity-90 group-hover:opacity-100' : 'opacity-100'
        ]" />

      </div>

    </div>

    <Transition name="fade">
      <div v-if="activeNode"
        class="absolute inset-0 flex flex-col items-center justify-center bg-black/80 backdrop-blur-md z-20 px-10">

        <div class="relative group max-w-2xl cursor-pointer" @click="activeNode = null">
          <img :src="activeNode.image"
            class="relative z-10 w-full drop-shadow-[0_0_100px_rgba(255,255,255,0.5)] group-hover:drop-shadow-[0_0_150px_rgba(255,255,255,0.8)] transition-all duration-700" />

        </div>
      </div>
    </Transition>

    <div class="absolute inset-0 pointer-events-none z-9 flex flex-col justify-center px-[10vw] space-y-4 mt-[11em]">
      <div class="w-fit px-6 py-4 border-l-2 border-white/10" oldclass=" bg-black/40 backdrop-blur-sm shadow-2xl">
        <h1
          class="text-white opacity-80 text-6xl md:text-6xl font-bold leading-none mix-blend-difference text-left drop-shadow-[0_0_10px_rgba(255,255,255,0.6)]">
          Un universo<br>
          <span class="text-white">que renace</span>
        </h1>
      </div>

      <p
        class="text-white opacity-80 text-6xl md:text-6xl font-bold leading-none mix-blend-difference text-right mt-[6rem] drop-shadow-[0_0_10px_rgba(255,255,255,0.6)]">
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

  0%,
  100% {
    transform: translate(-50%, -52%);
  }

  50% {
    transform: translate(-50%, -48%);
  }
}

/* Retraso aleatorio para que no se muevan todas iguales */
.absolute.group:nth-child(even) {
  animation-duration: 8s;
  animation-delay: 1s;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
