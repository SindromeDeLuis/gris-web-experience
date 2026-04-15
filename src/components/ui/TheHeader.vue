<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import gsap from 'gsap';

const platforms = [
  { name: 'Steam', src: 'images/icons/steam.svg', enlace: 'https://store.steampowered.com/app/683320/GRIS/' },
  { name: 'Switch', src: 'images/icons/switch.svg', enlace: 'https://www.nintendo.com/games/detail/gris-switch/' },
  { name: 'PlayStation', src: 'images/icons/playstation.svg', enlace: 'https://www.playstation.com/games/gris/' },
  { name: 'Xbox', src: 'images/icons/xbox.svg', enlace: 'https://www.xbox.com/en-us/games/store/gris/9n6c6j7c3gtq' },
  { name: 'App Store', src: 'images/icons/apple.svg', enlace: 'https://apps.apple.com/us/app/gris/id1445379072' },
];

const isMenuOpen = ref(false);

const navLinks = [
  { name: 'Inicio', path: '/' },
  { name: 'Historia', path: '/historia' },
  { name: 'Arte', path: '/arte' },
  { name: 'Música', path: '/musica' },
  { name: 'Gameplay', path: '/gameplay' },
  { name: '¡ADQUIERE GRIS!', path: '/tiendas' }
];

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
  // Bloquear scroll cuando el menú esté abierto
  document.body.style.overflow = isMenuOpen.value ? 'hidden' : '';
};

const isScrolled = ref(false);
// Cambiar el fondo del header al hacer scroll para que no se pierda con el arte claro
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50;
};

// Animaciones de Entrada (GSAP)
const enterMenu = (el, done) => {
  const tl = gsap.timeline({ onComplete: done });

  tl.fromTo(el, { opacity: 0 }, { opacity: 1, duration: 0.4, ease: "power2.out" });

  const links = el.querySelectorAll('.nav-link');

  tl.fromTo(links,
    { y: 20, opacity: 0 },
    { y: 0, opacity: 1, duration: 0.5, stagger: 0.08, ease: "power3.out" },
    "-=0.3"
  );
};

// Animaciones de Salida
const leaveMenu = (el, done) => {
  gsap.to(el, { opacity: 0, duration: 0.6, ease: "power2.in", onComplete: done });
};

onMounted(() => window.addEventListener('scroll', handleScroll));
onUnmounted(() => window.removeEventListener('scroll', handleScroll));
</script>

<template>
  <header :class="[
    'fixed top-0 left-0 w-full z-50 transition-all duration-700 px-8 py-6 flex items-center justify-between',
    isScrolled ? 'bg-black/90 backdrop-blur-xl border-b border-white/5 py-4' : 'bg-transparent'
  ]">
    <router-link to="/" class="flex-1 flex items-center gap-3">
      <img src="/images/icons/Nomada-Symbol.png" alt="" class="w-10 h-10" />
      <div class="flex flex-col">
        <span class="font-sans text-lg tracking-[0.2em] uppercase leading-none">Nomada</span>
        <span class="text-[8px] tracking-[0.5em] text-white/50 uppercase mt-1">Studio</span>
      </div>
    </router-link>


    <nav class="hidden xl:flex items-center gap-3 flex-1 justify-center">
      <a v-for="shop in platforms" :key="shop.name" :href="shop.enlace" target="_blank"
        class="group flex items-center gap-3 border border-white/50 pl-2 pr-6 py-2 whitespace-nowrap hover:border-white/40 hover:bg-white/80 hover:text-black transition-all duration-600">
        <img :src="shop.src" :alt="shop.name"
          class="w-5 h-5 opacity-80 group-hover:opacity-100 transition-opacity invert group-hover:invert-0" />
        <span class="text-[10px] tracking-[0.4em] text-white/80 group-hover:text-black uppercase transition-colors">
          {{ shop.name }}
        </span>
      </a>
    </nav>


    <div class="flex-1 flex justify-end items-center gap-6">
      <button class="relative group px-6 py-2 overflow-hidden border border-white/50 cursor-pointer">
        <span
          class="relative z-10 text-[10px] tracking-[0.4em] uppercase group-hover:text-black transition-colors duration-500">
          Mirar Tráiler
        </span>
        <div
          class="absolute inset-0 bg-white translate-y-full group-hover:translate-y-0 transition-transform duration-500">
        </div>
      </button>

      <button @click="toggleMenu" class="relative z-[110] w-10 h-10 flex flex-col justify-center items-end gap-1.5 group cursor-pointer">
        <div :class="['w-7 h-[1.5px] bg-white/70 group-hover:bg-white transition-all duration-600', isMenuOpen ? 'rotate-45 translate-y-[7px]' : '']"></div>
        <div :class="['w-7 h-[1.5px] bg-white/70 group-hover:bg-white transition-all duration-600', isMenuOpen ? 'opacity-0' : '']"></div>
        <div :class="['h-[1.5px] bg-white/70 group-hover:bg-white transition-all duration-600', isMenuOpen ? 'w-7 -rotate-45 -translate-y-[7px]' : 'w-4 group-hover:w-7 self-end']"></div>
      </button>

      <transition @enter="enterMenu" @leave="leaveMenu">
      <div v-show="isMenuOpen" class="menu-wrapper fixed inset-0 z-[105]">
        <div class="absolute inset-0 bg-gradient-to-b from-black/40 to-black/80"></div>

        <nav class="side-panel absolute top-0 right-0 h-full w-full max-w-sm bg-white/[0.5] border-l border-white/5 flex flex-col justify-center px-16 gap-8">
          <router-link
            v-for="(link, index) in navLinks"
            :key="index"
            :to="link.path"
            @click="isMenuOpen = false"
            class="nav-link text-black/60 text-3xl font-medium font-sans tracking-[0.15em] uppercase text-center opacity-0 transition-all duration-500 hover:text-black/80 hover:underline hover:underline-offset-4 hover:drop-shadow-[0_0_10px_rgba(255,255,255,0.6)]"
          >
            {{ link.name }}
          </router-link>
        </nav>
      </div>
    </transition>

    </div>
  </header>
</template>

<style scoped>
/* El texto de "Gris" y el botón deben estar por encima del blur */
header > * {
  -webkit-font-smoothing: antialiased;
}

header span {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
}

.menu-overlay {
  z-index: 105;
}

.nav-link {
  /* Sombra suave para mejorar legibilidad sobre el blur */
  text-shadow: 0 0 20px rgba(255, 255, 255, 0.1);
}
</style>
