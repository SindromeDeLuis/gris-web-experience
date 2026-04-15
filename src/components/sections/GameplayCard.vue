<script setup>
import { ref } from 'vue';

defineProps({
  title: String,
  description: String,
  ability: String,
  image: String
});

const isFlipped = ref(false);
</script>

<template>
  <div class="group h-80 w-64 [perspective:1000px] cursor-pointer" @click="isFlipped = !isFlipped">
    <div class="relative h-full w-full transition-all duration-700 [transform-style:preserve-3d]"
      :class="{ '[transform:rotateY(180deg)]': isFlipped }">

      <div class="absolute inset-0 m-auto h-full w-full rounded-3xl border border-white/10
              overflow-hidden backdrop-blur-[10px] bg-black/[0.15]
              flex flex-col items-center justify-center p-6
              shadow-[0_0_20px_rgba(255,255,255,0.6)]
              hover:shadow-[0_0_30px_rgba(255,255,255,0.8)] transition-shadow duration-500">
        <div class="absolute inset-0 bg-gradient-to-br from-blue-500/10 to-transparent"></div>

        <div class="relative w-32 h-32 mb-6 flex items-center justify-center">
          <img :src="image" :alt="ability" class="max-w-full max-h-full object-contain opacity-90">
        </div>

        <h3
          class="relative font-sans text-lg font-semibold tracking-[0.15em] uppercase text-center leading-tight text-white px-2">
          {{ ability }}
        </h3>
      </div>

      <div
        class="absolute inset-0 h-full w-full rounded-xl bg-white text-black p-8 [transform:rotateY(180deg)] [backface-visibility:hidden] flex flex-col justify-center">
        <h3 class="font-serif text-2xl mb-4 border-b border-black/10 pb-2">{{ title }}</h3>
        <p class="text-sm leading-relaxed font-medium italic">
          {{ description }}
        </p>
      </div>
    </div>
  </div>
</template>
