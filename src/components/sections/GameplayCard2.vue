<script setup>
import { ref } from 'vue';

defineProps({
  title: String,
  description: String,
  stat: String,
  image: String
});
</script>

<template>
  <div class="group h-64 w-136 [perspective:1000px] cursor-pointer">
    <div class="relative h-full w-full transition-all duration-700 [transform-style:preserve-3d]">
      <div class="absolute inset-0 m-auto h-full w-full rounded-3xl border border-white/10
              overflow-hidden backdrop-blur-[10px] bg-white/[0.05]
              flex flex-col items-center justify-center p-6
              shadow-[0_0_20px_rgba(255,255,255,0.6)]
              hover:shadow-[0_0_30px_rgba(255,255,255,0.8)] transition-shadow duration-500">
        <div class="absolute inset-0 bg-gradient-to-br from-blue-500/10 to-transparent"></div>

        <div class="relative w-40 h-40 flex items-center justify-center">
          <img :src="image" :alt="stat" class="max-w-full max-h-full object-contain opacity-90">
        </div>

        <h3
          class="relative font-sans text-lg font-semibold tracking-[0.15em] uppercase text-center leading-tight text-white px-2">
          {{ stat }}
        </h3>
        <p class="text-sm leading-relaxed font-medium">
          {{ description }}
        </p>
      </div>
    </div>
  </div>
</template>
