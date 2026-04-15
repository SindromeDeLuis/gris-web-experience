<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import { nodes } from '../../data/navigation';
import gsap from 'gsap';

const activeNode = ref(null);
const router = useRouter();

onMounted(() => {
  // Animación de entrada para las líneas de la constelación
  gsap.from(".constellation-line", {
    duration: 3,
    ease: "power2.out"
  });
});

// Animación de Hover con GSAP para que sea más fluida que CSS
const hoverStar = (el) => {
  gsap.to(el.querySelector('.star-core'), { r: 28, duration: 0.4, ease: "back.out(2)" });
  gsap.to(el.querySelector('.star-halo'), { r: 36, opacity: 0.5, duration: 0.4 });
  gsap.to(el.querySelector('.star-aura'), { r: 44, opacity: 0.3, duration: 0.6 });
};

const leaveStar = (el) => {
  gsap.to(el.querySelector('.star-core'), { r: 24, duration: 0.4 });
  gsap.to(el.querySelector('.star-halo'), { r: 30, opacity: 0.2, duration: 0.4 });
  gsap.to(el.querySelector('.star-aura'), { r: 36, opacity: 0.1, duration: 0.4 });
};

const selectNode = (node) => {
  activeNode.value = node;
};

const navigateToSection = (nodeId) => {
  // Cerramos el modal antes de irnos para que no estorbe al volver
  activeNode.value = null;
  router.push({ name: nodeId });
};
</script>

<template>
  <div class="relative w-full h-screen flex items-center justify-center overflow-hidden">

    <svg class="absolute invisible">
      <defs>
        <filter id="glow">
          <feGaussianBlur stdDeviation="3" result="coloredBlur" />
          <feMerge>
            <feMergeNode in="coloredBlur" />
            <feMergeNode in="SourceGraphic" />
          </feMerge>
        </filter>
      </defs>
    </svg>

    <svg viewBox="0 0 1000 400" class="w-full max-w-5xl z-10 drop-shadow-2xl">
      <polyline points="80,200 150,250 250,150 450,180 650,120 900,270" fill="none" stroke="white" stroke-width="3"
        class="constellation-line" />

      <g v-for="node in nodes" :key="node.id" @click="selectNode(node)" @mouseenter="hoverStar($event.currentTarget)"
        @mouseleave="leaveStar($event.currentTarget)" class="cursor-pointer group">
        <circle :cx="node.x" :cy="node.y" r="36" fill="white" class="star-aura opacity-10 transition-all duration-600"
          style="opacity: 0.1;" />

        <circle :cx="node.x" :cy="node.y" r="30" fill="white" class="star-halo opacity-20 transition-all duration-500"
          style="filter: blur(3px);" />

        <circle :cx="node.x" :cy="node.y" r="24" fill="white" class="star-core shadow-white transition-all duration-300"
          style="filter: url(#glow);" />

        <text :x="node.x" :y="node.y + 45" text-anchor="middle" fill="white"
          class="text-[11px] tracking-[0.2em] opacity-0 group-hover:opacity-100 transition-all duration-300 uppercase">
          {{ node.name }}
        </text>
      </g>
    </svg>

    <Transition name="fade">
      <div v-if="activeNode"
        class="absolute inset-0 flex flex-col items-center justify-center bg-black/80 bg-black/90 z-20 px-10">

        <div @click="navigateToSection(activeNode.id)" class="relative group max-w-2xl cursor-pointer">
          <img :src="activeNode.image"
            class="relative z-10 w-full rounded-[28px] border border-white/20 shadow-[0_0_100px_rgba(255,255,255,0.5)] group-hover:shadow-[0_0_150px_rgba(255,255,255,0.8)] transition-all duration-700" />
          <div class="absolute inset-0 bg-gradient-to-t from-black/80 to-transparent"></div>
        </div>

        <h2 class="mt-8 text-white font-serif text-4xl tracking-[0.1em] uppercase">{{ activeNode.name }}</h2>
        <p class="mt-4 text-white/40 text-sm tracking-[0.1em] uppercase max-w-xl text-center leading-loose">
          {{ activeNode.subtitle || 'Explora este fragmento del universo' }}
        </p>

        <button @click="activeNode = null" class="mt-6 group flex flex-col items-center cursor-pointer">
          <span
            class="text-white/30 group-hover:text-white text-[10px] tracking-[0.4em] uppercase transition-colors">Volver</span>
          <div class="w-[1px] h-8 bg-white/20 group-hover:bg-white mt-2 transition-all"></div>
        </button>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
