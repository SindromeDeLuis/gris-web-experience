<template>
  <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-3 gap-6">
    <a v-for="store in stores" :key="store.name" :href="store.url" target="_blank" class="group relative flex flex-col items-center justify-center px-8 pt-8 pb-6 rounded-2xl
                border border-white/10 bg-black/[0.2] backdrop-blur-[5px] transition-all
                duration-500 hover:bg-black/[0.08] hover:border-black/20 hover:scale-105
                shadow-[0_0_20px_rgba(255,255,255,0.6)]
                hover:shadow-[0_0_30px_rgba(255,255,255,0.8)]">
      <div
        class="absolute inset-0 bg-gradient-to-br from-black/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity rounded-2xl">
      </div>

      <!--<div
            class="relative w-12 h-12 mb-6 flex items-center justify-center grayscale group-hover:grayscale-0 transition-all duration-500">
            <img :src="store.icon" :alt="store.name" class="max-w-full max-h-full object-contain">
          </div>-->

      <p class="text-white/80 text-2xl font-semibold mb-2">
        {{ store.name }}
      </p>

      <span class="relative text-lg tracking-wide text-white/70 group-hover:text-white transition-colors">
        {{ store.subtitle }}
      </span>
      <span
        class="relative text-sm font-light text-white/70 mt-2 group-hover:text-white group-hover:font-medium transition-colors">
        Ver en tienda
      </span>
    </a>
  </div>
</template>

<script setup>
const stores = [
  { name: 'Steam', subtitle: 'PC • Mac • Linux', icon: '/images/icons/steam.svg', url: '#' },
  { name: 'Nintendo Shop', subtitle: 'Nintendo Switch', icon: '/images/icons/switch.svg', url: '#' },
  { name: 'PlayStation', subtitle: 'PlayStation 4 • PlayStation 5', icon: '/images/icons/ps.svg', url: '#' },
  { name: 'Xbox', subtitle: 'Xbox One • Xbox Series X/S', icon: '/images/icons/xbox.svg', url: '#' },
  { name: 'App Store', subtitle: 'iPhone • iPad', icon: '/images/icons/apple.svg', url: '#' },
  { name: 'Google Play Store', subtitle: 'Android', icon: '/images/icons/google-play.svg', url: '#' },
]
</script>
