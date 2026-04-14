<script setup>
import { onMounted } from 'vue';
import Lenis from 'lenis';
import TheHeader from './components/ui/TheHeader.vue';

onMounted(() => {
  const lenis = new Lenis({
    duration: 1.2,
    easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
  });

  function raf(time) {
    lenis.raf(time);
    requestAnimationFrame(raf);
  }
  requestAnimationFrame(raf);
});
</script>

<template>
  <TheHeader />

  <router-view v-slot="{ Component }">
    <transition name="page-fade" mode="out-in">
      <component :is="Component" />
    </transition>
  </router-view>
</template>

<style>
/* Transición suave entre páginas de la web */
.page-fade-enter-active,
.page-fade-leave-active {
  transition: opacity 0.8s ease, filter 0.8s ease;
}

.page-fade-enter-from,
.page-fade-leave-to {
  opacity: 0;
  filter: blur(10px);
}
</style>
