<script setup>
import { onMounted } from 'vue';
import gsap from 'gsap';

onMounted(() => {
  const tl = gsap.timeline();

  // Animación de entrada: El título aparece con un ligero desenfoque y escala
  tl/*.from(".hero-title", {
    opacity: 0,
    filter: "blur(20px)",
    scale: 1.1,
    duration: 2.5,
    ease: "power2.out"
  })*/
    .from(".hero-subtitle", {
      opacity: 0,
      y: 20,
      duration: 1.5,
      ease: "power2.out"
    }, "-=1.5")
    .from(".hero-btn", {
      opacity: 0,
      duration: 1,
    }, "-=0.5");
});

const scrollToRecorrido = () => {
  const target = document.getElementById('recorrido');
  if (target) {
    target.scrollIntoView({ behavior: 'smooth' });
  }
};
</script>

<template>
  <section class="relative h-screen w-full flex flex-col items-center justify-center overflow-hidden">

    <div class="relative z-10 text-center px-4">


    </div>

    <div class="absolute bottom-24 z-10">
      <button @click="scrollToRecorrido"
        class="hero-btn group relative px-10 py-3 overflow-hidden flex items-center justify-center">
        <span
          class="absolute inset-0 border border-white rounded-full group-hover:border-white group-hover:bg-white transition-colors duration-500"></span>

        <span
          class="relative text-[13px] lg:text-[12px] font-semibold lg:font-normal tracking-[0.1em] lg:tracking-[0.6em] uppercase text-white group-hover:text-black transition-all duration-500 whitespace-nowrap pl-[0.8em]">
          Iniciar el recorrido
        </span>
      </button>
    </div>

    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 opacity-20">
      <div class="w-[1px] h-10 bg-white"></div>
    </div>
  </section>
</template>

<style scoped>
/* Ajuste para que la tipografía se vea más fina en pantallas retina */
.hero-title {
  isolation: isolate;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  -webkit-font-smoothing: antialiased;
  text-shadow: 0 0 30px rgba(255, 255, 255, 0.1);
}

.hero-subtitle {
  /* Forzamos a la GPU a renderizar esto como una capa independiente */
  transform: translateZ(0);
  will-change: opacity, transform;
}
</style>
