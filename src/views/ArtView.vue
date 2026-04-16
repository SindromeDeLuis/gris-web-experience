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
  <section class="relative w-full h-screen overflow-x-auto overflow-y-hidden bg-black flex">

    <div class="relative h-full w-[300vw] lg:w-full flex-shrink-0">

      <div class="absolute inset-0 z-0">
        <img src="/images/art-bg.png" class="w-full h-full object-cover" alt="Background Forest" />
      </div>

      <div v-for="piece in artPieces" :key="piece.id"
        class="art-piece-container absolute transform -translate-x-1/2 -translate-y-1/2 transition-all duration-700 hover:scale-105 cursor-pointer group"
        :style="{
          left: piece.x + '%',
          top: piece.y + '%',
          '--base-w': piece.width
        }">
        <img @click="selectNode(piece)" :src="piece.src" :class="[
          'w-full h-auto transition-all duration-500',
          piece.blur ? 'blur-[8px] group-hover:blur-0 opacity-90 group-hover:opacity-100' : 'opacity-100'
        ]" />
      </div>

    </div>

    <Transition name="fade">
      <div v-if="activeNode"
        class="fixed inset-0 flex flex-col items-center justify-center bg-black/80 backdrop-blur-md z-20 px-10">

        <div class="relative group max-w-2xl cursor-pointer" @click="activeNode = null">
          <img :src="activeNode.image"
            class="relative z-10 w-full drop-shadow-[0_0_100px_rgba(255,255,255,0.5)] group-hover:drop-shadow-[0_0_150px_rgba(255,255,255,0.8)] transition-all duration-700" />

        </div>
      </div>
    </Transition>

    <div
      class="fixed inset-0 pointer-events-none z-15 flex flex-col justify-evenly lg:justify-center px-4 md:px-[10vw] space-y-4">
      <div class="w-fit px-6 py-4 lg:mt-[10rem]">
        <h1
          class="text-white opacity-80 text-4xl md:text-6xl font-bold leading-none mix-blend-difference text-left drop-shadow-[0_0_10px_rgba(255,255,255,0.6)]">
          Un<br class="block md:hidden">
          universo<br>
          <span class="text-white">que renace</span>
        </h1>
      </div>
      <p
        class="text-white opacity-80 text-4xl md:text-6xl font-bold leading-none mix-blend-difference text-right mt-[6rem] drop-shadow-[0_0_10px_rgba(255,255,255,0.6)]">
        en cada textura
      </p>
    </div>

    <div class="fixed bottom-12 lg:left-24 z-20 px-6 md:px-0">
      <p class="text-white/70 text-sm tracking-[0.1em] uppercase font-medium text-center lg:text-left">
        Descubre los secretos que guardan los árboles
      </p>
    </div>

  </section>
</template>

<style scoped>
/* Ocultar scrollbar para estética de juego */
section {
  scrollbar-width: none;
  -ms-overflow-style: none;
}

section::-webkit-scrollbar {
  display: none;
}

/* El truco del Parallax: */
.relative.h-full.w-\[300vw\] {
  /* Creamos una perspectiva para el contenedor */
  perspective: 1px;
  perspective-origin: center;
}

.absolute.inset-0.z-0 {
  /* Si mueves el fondo "hacia atrás" en el eje Z y lo escalas,
     el scroll natural lo moverá más lento.
  */
  transform: translateZ(-1px) scale(2);
  transform-origin: center;
}

.art-piece-container {
  /* MÓVIL (Por defecto): Multiplicamos el ancho base para que no se vea minúsculo */
  /* Si piece.width es 10, aquí se verá como 30vw */
  width: calc(var(--base-w) * 3vw);
  min-width: 80px;
  /* Evita que desaparezcan si el valor es muy bajo */
}

/* TABLET (md) */
@media (min-width: 768px) {
  .art-piece-container {
    width: calc(var(--base-w) * 2vw);
  }
}

/* DESKTOP (xl) */
@media (min-width: 1280px) {
  .art-piece-container {
    width: calc(var(--base-w) * 1vw);
    max-width: 600px;
    /* Un tope para que no rompa la estética en pantallas ultra-wide */
  }
}

/* Tu animación de flotación se mantiene igual */
.art-piece-container {
  animation: float 8s ease-in-out infinite;
}
</style>
