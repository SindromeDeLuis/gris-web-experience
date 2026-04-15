<script setup>
import HeroHome from '../components/sections/HeroHome.vue';
import ConstellationNav from '../components/sections/ConstellationNav.vue';
</script>

<template>
  <div class="relative min-h-[200vh] bg-[#050505]">

    <div class="absolute inset-0 z-0 overflow-hidden">
      <img src="/images/home-bg.png" alt="GRIS Home Background"
        class="w-full h-full object-cover opacity-90 transition-transform duration-600 will-change-transform" />
      <div class="absolute inset-0 bg-gradient-to-b from-transparent via-black/20 to-[#050505]"></div>
    </div>

    <div class="relative z-10">
      <HeroHome id="home" />
      <ConstellationNav id="recorrido" />
    </div>
  </div>
</template>

<style scoped>
/* Evitamos que haya saltos visuales en el scroll */
:deep(section) {
  position: relative;
  height: 100vh;
  width: 100%;
}
</style>
