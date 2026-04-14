<script setup>
import { onMounted } from 'vue';
import Lenis from 'lenis';
import TheHeader from './components/ui/TheHeader.vue';
import HeroHome from './components/sections/HeroHome.vue';
import ConstellationNav from './components/sections/ConstellationNav.vue';

onMounted(() => {
  const lenis = new Lenis();
  function raf(time) {
    lenis.raf(time);
    requestAnimationFrame(raf);
  }
  requestAnimationFrame(raf);
});
</script>

<template>
  <TheHeader />

  <main>
    <HeroHome id="home" />

    <ConstellationNav id="recorrido" />

    </main>
</template>
