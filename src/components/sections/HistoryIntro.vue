<script setup>
import { onMounted, ref, onUnmounted } from 'vue';
import gsap from 'gsap';

const shadowRef = ref(null);
const containerRef = ref(null);

const features = [
  { title: 'Sin Diálogos', desc: 'Narrativa puramente visual que trasciende el lenguaje.', color: "lg:text-white" },
  { title: 'Sin Muerte', desc: 'Una experiencia relajada y serena centrada en el viaje.', color: "text-black/90" },
  { title: 'Arte a Mano', desc: 'Cada frame es una acuarela pintada con delicadeza.', color: "text-black/90" }
];

// Lógica de la Sombra que te imita
const handleMouseMove = (e) => {
  const { clientX, clientY } = e;

  // La sombra sigue al ratón con un suavizado (GSAP lo hace fácil)
  gsap.to(shadowRef.value, {
    x: clientX - 50,
    y: clientY - 50,
    duration: 1.5, // El retraso le da el toque "fantasmagórico"
    ease: "power2.out"
  });
};

onMounted(() => {
  window.addEventListener('mousemove', handleMouseMove);

  // Animación de aparición de los textos
  gsap.from(".history-item", {
    scrollTrigger: ".history-content",
    y: 50,
    opacity: 0,
    stagger: 0.3,
    duration: 1.5,
    ease: "power3.out"
  });
});

onUnmounted(() => {
  window.removeEventListener('mousemove', handleMouseMove);
});
</script>

<template>
  <div ref="containerRef"
    class="relative min-h-screen text-white overflow-hidden flex flex-col items-center justify-evenly md:justify-center py-10 lg:py-20 px-4 lg:px-6">

    <div ref="shadowRef"
      class="pointer-events-none fixed top-0 left-0 w-32 h-32 z-0 opacity-20 blur-2xl rounded-full bg-white"></div>

    <div class="relative z-10 max-w-6xl w-full">
      <header class="text-center mb-10 lg:mb-70">
        <h2
          class="font-sans text-[17px] md:text-5xl tracking-[0.02em] font-bold mb-1 drop-shadow-[0_0_10px_rgba(255,255,255,0.8)]">
          Una experiencia de juego única
        </h2>
        <p
          class="text-white/70 text-lg md:text-3xl tracking-wide leading-none max-w-3xl mx-auto drop-shadow-[0_0_10px_rgba(255,255,255,0.8)]">
          que combina arte, musica y narrativa emocional
        </p>
      </header>
    </div>

    <footer class="relative md:absolute lg:bottom-20 w-full flex justify-center px-6">
      <div class="relative w-full max-w-7xl">

        <!-- Capa efecto detrás del contenido -->
        <div class="absolute inset-0 -z-10 rounded-4xl pointer-events-none">
          <!-- 1) Glow externo (siempre visible) -->
          <div class="hidden md:block absolute inset-0 rounded-4xl
                      shadow-[0_0_20px_rgba(255,255,255,1),0_0_20px_rgba(255,255,255,1)]">
          </div>

          <!-- 2) Panel blanco con borde que se vuelve transparente (se ve el fondo real) -->
          <div class="absolute inset-0 rounded-4xl bg-white
                      shadow-[inset_0_0_0_1px_rgba(255,80,80,0.18),inset_0_0_35px_rgba(255,80,80,0.10)]
                      [--fade:6px]
                      [-webkit-mask-image:linear-gradient(to_right,transparent_0,black_var(--fade),black_calc(100%-var(--fade)),transparent_100%),linear-gradient(to_bottom,transparent_0,black_var(--fade),black_calc(100%-var(--fade)),transparent_100%)]
                      [-webkit-mask-composite:source-in]
                      [mask-image:linear-gradient(to_right,transparent_0,black_var(--fade),black_calc(100%-var(--fade)),transparent_100%),linear-gradient(to_bottom,transparent_0,black_var(--fade),black_calc(100%-var(--fade)),transparent_100%)]
                      [mask-composite:intersect]">
          </div>
        </div>
        <div class="history-content grid grid-cols-1 md:grid-cols-3 gap-4 md:gap-8 py-10 px-12 relative z-10">
          <div v-for="item in features" :key="item.title"
            class="history-item group flex flex-col items-center text-center">
            <h3
              :class="['history-item font-sans text-2xl tracking-[0.02em] font-semibold uppercase mb-2 text-black/90', item.color]">
              {{ item.title }}
            </h3>
            <p :class="['hidden lg:block leading-relaxed tracking-wide text-base max-w-xs font-medium', item.color]">
              {{ item.desc }}
            </p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>
