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
  <div
    class="group h-80 w-64 [perspective:1000px] cursor-pointer"
    @click="isFlipped = !isFlipped"
  >
    <div
      class="relative h-full w-full transition-all duration-700 [transform-style:preserve-3d]"
      :class="{ '[transform:rotateY(180deg)]': isFlipped }"
    >
      <div class="absolute inset-0 h-full w-full rounded-xl border border-white/10 bg-white/5 flex flex-col items-center justify-center p-4 [backface-visibility:hidden]">
        <div class="w-20 h-20 mb-4 opacity-80 bg-white/10 rounded-full flex items-center justify-center">
           <span class="text-2xl">✨</span>
        </div>
        <h3 class="font-serif text-xl tracking-widest uppercase text-center">{{ ability }}</h3>
      </div>

      <div class="absolute inset-0 h-full w-full rounded-xl bg-white text-black p-8 [transform:rotateY(180deg)] [backface-visibility:hidden] flex flex-col justify-center">
        <h3 class="font-serif text-2xl mb-4 border-b border-black/10 pb-2">{{ title }}</h3>
        <p class="text-sm leading-relaxed font-light italic">
          {{ description }}
        </p>
      </div>
    </div>
  </div>
</template>
