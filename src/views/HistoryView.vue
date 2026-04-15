<script setup>
import HistoryIntro from '../components/sections/HistoryIntro.vue';
import HistoryStars from '../components/sections/HistoryStars.vue';
</script>

<template>
  <div class="relative min-h-[200vh]">

    <div class="absolute inset-0 -z-11 overflow-hidden">
      <img src="/images/history-bg.png" alt="GRIS History Background"
        class="w-full h-full object-cover transition-transform duration-600 will-change-transform" />
    </div>

    <div class="absolute inset-0 z-0 overflow-hidden">
      <img src="/images/history-bg2.png"
        class="w-full h-full object-cover transition-transform duration-600 will-change-transform" id="parallax-bg-2" />
    </div>

    <HistoryIntro />
    <HistoryStars />
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
