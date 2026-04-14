<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const isScrolled = ref(false);
const isMenuOpen = ref(false);
// Cambiar el fondo del header al hacer scroll para que no se pierda con el arte claro
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50;
};

onMounted(() => window.addEventListener('scroll', handleScroll));
onUnmounted(() => window.removeEventListener('scroll', handleScroll));

const platforms = [
  { name: 'Steam', src: 'images/icons/steam.svg' },
  { name: 'Switch', src: 'images/icons/switch.svg' },
  { name: 'PlayStation', src: 'images/icons/playstation.svg' },
  { name: 'Xbox', src: 'images/icons/xbox.svg' },
  { name: 'App Store', src: 'images/icons/apple.svg' },
];
</script>

<template>
  <header
    :class="[
      'fixed top-0 left-0 w-full z-50 transition-all duration-700 px-8 py-6 flex items-center justify-between',
      isScrolled ? 'bg-black/90 backdrop-blur-xl border-b border-white/5 py-4' : 'bg-transparent'
    ]"
  >
    <div class="flex-1 flex items-center gap-3">
      <img src="/images/icons/Nomada-Symbol.png" alt="" class="w-10 h-10" />
      <div class="flex flex-col">
        <span class="font-serif text-lg tracking-[0.4em] uppercase leading-none">Nomada</span>
        <span class="text-[8px] tracking-[0.5em] text-white/50 uppercase mt-1">Studio</span>
      </div>
    </div>


      <nav class="hidden xl:flex items-center gap-3 flex-1 justify-center">
        <a
          v-for="shop in platforms"
          :key="shop.name"
          href="#"
          class="group flex items-center gap-3 border border-white/50 pl-2 pr-6 py-2 whitespace-nowrap hover:border-white/40 hover:bg-white/80 hover:text-black transition-all duration-600"
        >
          <img
            :src="shop.src"
            :alt="shop.name"
            class="w-5 h-5 opacity-80 group-hover:opacity-100 transition-opacity invert group-hover:invert-0"
          />
          <span class="text-[10px] tracking-[0.4em] text-white/80 group-hover:text-black uppercase transition-colors">
            {{ shop.name }}
          </span>
        </a>
      </nav>


      <div class="flex-1 flex justify-end items-center gap-6">
        <button class="relative group px-6 py-2 overflow-hidden border border-white/50">
          <span class="relative z-10 text-[10px] tracking-[0.4em] uppercase group-hover:text-black transition-colors duration-500">
            Mirar Tráiler
          </span>
          <div class="absolute inset-0 bg-white translate-y-full group-hover:translate-y-0 transition-transform duration-500"></div>
        </button>

        <button
          @click="isMenuOpen = !isMenuOpen"
          class="flex flex-col gap-1.5 p-2 group"
        >
          <div class="w-6 h-[1px] bg-white/70 group-hover:bg-white transition-all"></div>
          <div class="w-6 h-[1px] bg-white/70 group-hover:bg-white transition-all"></div>
          <div class="w-4 h-[1px] bg-white/70 group-hover:w-6 group-hover:bg-white transition-all self-end"></div>
        </button>

    </div>
  </header>
</template>

<style scoped>
header span {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
}
</style>
