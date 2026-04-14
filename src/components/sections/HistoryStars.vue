<script setup>
import { ref } from 'vue';
import gsap from 'gsap';

const activeNode = ref(null);

const historyNodes = [
  { id: 1, x: 15, y: 15, title: 'El mundo se cae a pedazos', size: 'extra-large' },
  { id: 2, x: 20, y: 50, title: 'El desierto rojo de la Ira', size: 'large' },
  { id: 3, x: 40, y: 25, title: 'Un amigo de piedra y manzanas', size: 'extra-large' },
  { id: 4, x: 35, y: 60, title: 'La transformación del vestido', size: 'large' },
  { id: 5, x: 70, y: 15, title: 'El bosque que cambia de forma', size: 'large' },
  { id: 6, x: 65, y: 75, title: 'Cantar para florecer', size: 'medium' },
  { id: 7, x: 60, y: 40, title: 'La tortuga de cristal', size: 'large' },
  { id: 8, x: 77, y: 36, title: 'La sombra que te imita', size: 'medium' },
  { id: 9, x: 80, y: 65, title: 'El castillo de luz', size: 'large' },
  { id: 10, x: 85, y: 10, title: 'La estatua rota', size: 'large' },
];

const onEnter = (node, el) => {
  activeNode.value = node;
  gsap.to(el.querySelectorAll('.ring'), {
    scale: 1.5,
    opacity: 0,
    stagger: 0.2,
    duration: 1,
    repeat: -1
  });
};

const onLeave = (el) => {
  activeNode.value = null;
  gsap.killTweensOf(el.querySelectorAll('.ring'));
  gsap.to(el.querySelectorAll('.ring'), { scale: 1, opacity: 0.5, duration: 0.5 });
};
</script>

<template>
  <section class="relative w-full h-screen overflow-hidden flex items-center justify-center">

<div class="absolute inset-0 m-auto -z-10 w-[90dvw] h-[90dvh] pointer-events-none border border-white/20 rounded-[2rem] overflow-hidden backdrop-blur-[10px] bg-white/[0.03] shadow-[0_0_20px_rgba(255,255,255,0.6),0_0_20px_rgba(255,255,255,0.6)]">

    <div class="absolute inset-0 bg-gradient-to-br from-red-500/10 to-transparent"></div>

</div>

    <div class="absolute top-12 left-24 z-20">
      <p class="text-white/70 text-sm tracking-[0.1em] uppercase font-medium">
        Explora las estrellas con el cursor
      </p>
    </div>

    <div class="relative w-full h-full max-w-7xl max-h-[90vh]">
      <div
        v-for="node in historyNodes"
        :key="node.id"
        class="absolute group cursor-pointer"
        :style="{ left: node.x + '%', top: node.y + '%' }"
        @mouseenter="onEnter(node, $event.currentTarget)"
        @mouseleave="onLeave($event.currentTarget)"
      >
        <div class="ring absolute inset-0 border border-white/40 rounded-full scale-130"></div>
        <div class="ring absolute inset-0 border border-white/20 rounded-full scale-170"></div>

        <div
          :class="[
            'bg-white rounded-full shadow-[0_0_20px_white] transition-transform duration-500 group-hover:scale-125',
            node.size === 'extra-large' ? 'w-16 h-16' : node.size === 'large' ? 'w-12 h-12' : 'w-8 h-8'
          ]"
        ></div>

        <Transition name="slide-fade">
          <div
            v-if="activeNode?.id === node.id"
            class="absolute left-full ml-4 top-1/2 -translate-y-1/2 whitespace-nowrap z-30"
          >
            <div class="bg-[#2d121b]/90 backdrop-blur-md px-6 py-2.5 rounded-full border border-white/10 shadow-2xl">
              <span class="text-white/90 tracking-wide text-lg font-semibold">{{ node.title }}</span>
            </div>
          </div>
        </Transition>
      </div>
    </div>

    <div class="absolute bottom-12 left-24 z-20">
      <p class="text-white/70 text-sm tracking-[0.1em] uppercase font-medium">
        Encuentra detalles sobre el viaje de GRIS
      </p>
    </div>
  </section>
</template>

<style scoped>
.slide-fade-enter-active { transition: all 0.3s ease-out; }
.slide-fade-leave-active { transition: all 0.2s cubic-bezier(1, 0.5, 0.8, 1); }
.slide-fade-enter-from, .slide-fade-leave-to {
  transform: translateX(-10px) translateY(-50%);
  opacity: 0;
}

.ring {
  transition: all 0.5s ease;
}

@keyframes softPulse {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 0.6; }
}
.ring {
  animation: softPulse 4s infinite ease-in-out;
}
</style>
