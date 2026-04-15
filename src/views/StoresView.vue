<template>
  <section class="relative w-full h-screen flex flex-col items-center justify-center overflow-hidden bg-black">

    <div class="absolute inset-0 z-0">
      <img src="/images/stores-bg.png" class="w-full h-full object-cover" alt="Background Forest" />
    </div>

    <div class="absolute inset-0 z-0">
      <div class="absolute top-[-10%] left-[-5%] w-[600px] h-[600px] bg-blue-900/20 blur-[150px] rounded-full"></div>
      <div class="absolute bottom-[-10%] right-[-5%] w-[500px] h-[500px] bg-red-900/20 blur-[150px] rounded-full"></div>
    </div>

    <div class="relative z-10 w-full max-w-6xl px-6">

      <div class="text-center mb-16">
        <h2
          class="text-white/80 font-sans text-4xl md:text-5xl font-bold uppercase mix-blend-difference drop-shadow-[0_0_10px_rgba(255,255,255,0.8)]">
          Disponible en
        </h2>
        <p class="text-white/70 font-medium tracking-wide drop-shadow-[0_0_10px_rgba(255,255,255,0.8)]">
          ¡Experimenta GRIS en tu plataforma favorita!
        </p>
      </div>
    </div>

    <div class="relative z-10 w-full max-w-6xl px-6">
      <StoreLinks />
    </div>
  </section>
</template>

<script setup>
import StoreLinks from '../components/sections/StoreLinks.vue';
</script>
