<template>
  <section class="min-h-screen bg-[#0a0a0a] py-20 px-6 overflow-hidden">
    <div class="max-w-6xl mx-auto text-center mb-16">
      <h2 class="font-serif text-4xl md:text-5xl tracking-widest uppercase mb-4">
        Habilidades de Juego
      </h2>
      <p class="text-white/50 font-light italic tracking-wide">
        Mecánicas simples que crean experiencias profundas
      </p>
    </div>

    <div class="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 justify-items-center mb-24">
      <GameplayCard
        v-for="item in abilities"
        :key="item.id"
        v-bind="item"
      />
    </div>

    <div class="max-w-5xl mx-auto border-t border-white/10 pt-16">
      <div class="grid grid-cols-2 md:grid-cols-4 gap-12 text-center">
        <div class="space-y-3">
          <h4 class="font-serif text-lg tracking-widest uppercase">Plataformas</h4>
          <p class="text-xs text-white/40 leading-relaxed">Navega a través de estructuras arquitectónicas</p>
        </div>
        <div class="space-y-3">
          <h4 class="font-serif text-lg tracking-widest uppercase">Puzzles</h4>
          <p class="text-xs text-white/40 leading-relaxed">Resuelve enigmas únicos</p>
        </div>
        <div class="space-y-3">
          <h4 class="font-serif text-lg tracking-widest uppercase">Exploración</h4>
          <p class="text-xs text-white/40 leading-relaxed">Descubre secretos ocultos en cada rincón</p>
        </div>
        <div class="space-y-3">
          <h4 class="font-serif text-lg tracking-widest uppercase">Coleccionables</h4>
          <p class="text-xs text-white/40 leading-relaxed">Encuentra estrellas para abrir nuevos caminos</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import GameplayCard from './GameplayCard.vue';
import { onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

const abilities = [
  {
    id: 1,
    ability: "Convertirse en Cubo",
    title: "Mecánica de Peso",
    description: "Gris se transforma en un bloque pesado para resistir vientos huracanados y romper suelos agrietados.",
    icon: "🧱" // Puedes sustituir por un SVG o imagen
  },
  {
    id: 2,
    ability: "Saltar muy alto",
    title: "Doble Salto",
    description: "Utiliza el impulso de las aves para alcanzar estructuras elevadas y navegar por el cielo.",
    icon: "🕊️"
  },
  {
    id: 3,
    ability: "Nadar",
    title: "Fluidez",
    description: "Muévete con libertad en los entornos acuáticos, explorando las profundidades del universo.",
    icon: "💧"
  },
  {
    id: 4,
    ability: "Volar",
    title: "Ascensión",
    description: "Planea suavemente para recorrer distancias largas y descubrir secretos ocultos.",
    icon: "✨"
  }
];

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  gsap.from(".group", {
    scrollTrigger: ".grid",
    y: 50,
    opacity: 0,
    duration: 1,
    stagger: 0.2, // Hace que aparezcan una tras otra
    ease: "power2.out"
  });
});
</script>
