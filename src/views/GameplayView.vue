<template>
  <section
    class="relative z-0 w-full min-h-[200vh] bg-[#0a0a0a] flex flex-col justify-center py-20 px-6 overflow-hidden">

    <div class="absolute inset-0 -z-11 overflow-hidden">
      <img src="/images/gameplay-bg.png" alt="GRIS Gameplay Background"
        class="w-full h-full object-cover scale-105 transition-transform duration-1000" />
    </div>

    <div class="relative z-10 max-w-6xl mx-auto w-full">

      <div class="text-center my-16">
        <h2
          class="text-white/80 font-sans text-4xl md:text-5xl font-bold uppercase mix-blend-difference drop-shadow-[0_0_10px_rgba(255,255,255,0.8)]">
          HABILIDADES DE JUEGO
        </h2>
        <p class="text-white/70 font-medium tracking-wide drop-shadow-[0_0_10px_rgba(255,255,255,0.8)]">
          Mecánicas simples que crean experiencias profundas
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 justify-items-center mb-20">
        <GameplayCard v-for="item in abilities" :key="item.id" v-bind="item" class="gameplay-card" />
      </div>

      <div class="text-center my-8">
        <h2
          class="text-white/70 font-sans text-4xl md:text-5xl font-bold uppercase mix-blend-difference drop-shadow-[0_0_10px_rgba(255,255,255,0.8)]">
          MECÁNICAS DE JUEGO
        </h2>
      </div>

      <<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-2 gap-8 justify-items-center mb-20">
        <GameplayCard2 v-for="item in stats" :key="item.id" v-bind="item" class="gameplay-card" />
    </div>
    </div>

    <div class="absolute inset-0 -z-10 bg-gradient-to-b from-black via-[#0f0505] to-black opacity-50"></div>
  </section>
</template>

<script setup>
import GameplayCard from '../components/sections/GameplayCard.vue';
import GameplayCard2 from '../components/sections/GameplayCard2.vue';
import { onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

const stats = [
  {
    id: 1,
    stat: "Plataformas",
    title: "Plataformas",
    description: "Navega a través de estructuras arquitectónicas",
    image: "/images/skills/plataformas-02.png"
  },
  {
    id: 2, stat: "Puzzles", title: "Puzzles", description: "Resuelve enigmas únicos",
    image: "/images/skills/puzzles-02.png"
  },
  {
    id: 3, stat: "Exploración", title: "Exploración", description: "Descubre secretos ocultos en cada rincón",
    image: "/images/skills/exploracion-02.png"
  },
  {
    id: 4, stat: "Estrellas", title: "Estrellas", description: "Encuentra estrellas para abrir nuevos caminos",
    image: "/images/skills/coleccionables-02.png"
  }
];

const abilities = [
  {
    id: 1,
    ability: "Convertirse en Cubo",
    title: "Mecánica de Peso",
    description: "Gris se transforma en un bloque pesado para resistir vientos huracanados y romper suelos agrietados.",
    image: "/images/skills/cubo-02.png" // Puedes sustituir por un SVG o imagen
  },
  {
    id: 2,
    ability: "Saltar muy alto",
    title: "Doble Salto",
    description: "Utiliza el impulso de las aves para alcanzar estructuras elevadas y navegar por el cielo.",
    image: "/images/skills/saltar-02.png"
  },
  {
    id: 3,
    ability: "Nadar",
    title: "Fluidez",
    description: "Muévete con libertad en los entornos acuáticos, explorando las profundidades del universo.",
    image: "/images/skills/nadar-02.png"
  },
  {
    id: 4,
    ability: "Volar",
    title: "Ascensión",
    description: "Planea suavemente para recorrer distancias largas y descubrir secretos ocultos.",
    image: "/images/skills/volar-02.png"
  }
];

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  // Cambiamos el selector a .gameplay-card para evitar conflictos con otras clases "group"
  gsap.from(".gameplay-card", {
    scrollTrigger: {
      trigger: ".grid",
      start: "top 80%",
    },
    y: 30,
    opacity: 0,
    duration: 1.2,
    stagger: 0.15,
    ease: "expo.out"
  });
});
</script>
