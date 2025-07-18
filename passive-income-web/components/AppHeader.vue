<template>
  <header class="bg-white dark:bg-neutral-darkest text-neutral-darkest dark:text-neutral-lightest shadow-sm py-3 relative z-20">
    <div class="container mx-auto flex justify-between items-center px-4">
      <NuxtLink to="/" class="flex items-center text-xl lg:text-2xl font-bold tracking-tight text-neutral-darkest dark:text-neutral-lightest hover:text-primary transition-colors duration-200">
        <span class="material-icons-outlined text-primary text-3xl lg:text-4xl mr-2">
          auto_graph
        </span>
        不労所得への道
      </NuxtLink>

      <nav class="hidden lg:block">
        <ul class="flex items-center space-x-2">
          <li v-for="link in navLinks" :key="link.to">
            <NuxtLink :to="link.to" class="relative py-2 px-4 group text-neutral-darkest dark:text-neutral-light hover:text-primary transition-colors duration-200 text-sm lg:text-base font-medium">
              {{ link.text }}
              <span :class="['absolute bottom-0 left-0 w-full h-0.5 bg-primary scale-x-0 group-hover:scale-x-100 transition-transform duration-300 origin-center', { 'scale-x-100': $route.path === link.to }]"></span>
            </NuxtLink>
          </li>
          <li>
            <button @click="toggleDarkMode" class="p-2 rounded-md hover:bg-neutral-light dark:hover:bg-neutral-dark transition-colors duration-200 flex items-center justify-center">
              <span v-if="isDarkMode" class="material-icons-outlined text-purple-400 text-2xl">dark_mode</span>
              <span v-else class="material-icons-outlined text-yellow-500 text-2xl">light_mode</span>
            </button>
          </li>
        </ul>
      </nav>

      <div class="lg:hidden flex items-center">
        <button @click="toggleDarkMode" class="p-2 rounded-md hover:bg-neutral-light dark:hover:bg-neutral-dark transition-colors duration-200 mr-2 flex items-center justify-center">
          <span v-if="isDarkMode" class="material-icons-outlined text-purple-400 text-2xl">dark_mode</span>
          <span v-else class="material-icons-outlined text-yellow-500 text-2xl">light_mode</span>
        </button>
        <button @click="toggleMenu" class="focus:outline-none p-2 rounded-md hover:bg-neutral-light dark:hover:bg-neutral-dark transition-colors duration-200">
          <svg class="h-6 w-6 text-neutral-dark dark:text-neutral-light" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path v-if="!isMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
    </div>

    <Transition
      enter-active-class="transition ease-out duration-200 transform"
      enter-from-class="-translate-y-full opacity-0"
      enter-to-class="translate-y-0 opacity-100"
      leave-active-class="transition ease-in duration-150 transform"
      leave-from-class="translate-y-0 opacity-100"
      leave-to-class="-translate-y-full opacity-0"
    >
      <div v-if="isMenuOpen" class="lg:hidden bg-white dark:bg-neutral-darkest shadow-lg absolute top-full left-0 w-full z-10">
        <nav class="px-4 py-3">
          <ul class="space-y-2">
            <li v-for="link in navLinks" :key="link.to">
              <NuxtLink @click="isMenuOpen = false" :to="link.to" class="block hover:bg-neutral-light dark:hover:bg-neutral-dark py-2 px-3 rounded-md transition duration-200 text-base font-medium text-neutral-darkest dark:text-neutral-lightest">
                {{ link.text }}
              </NuxtLink>
            </li>
          </ul>
        </nav>
      </div>
    </Transition>
  </header>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const isMenuOpen = ref(false);
const isDarkMode = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
  if (process.client) {
    if (isDarkMode.value) {
      document.documentElement.classList.add('dark');
      localStorage.setItem('theme', 'dark');
    } else {
      document.documentElement.classList.remove('dark');
      localStorage.setItem('theme', 'light');
    }
  }
};

const navLinks = [
  { to: '/articles', text: '記事' },
  { to: '/apps', text: 'アプリ' },
  { to: '/performance', text: '実績' },
  { to: '/about', text: 'サイトについて' },
  { to: '/contact', text: 'お問い合わせ' },
];

const route = useRoute();
watch(route, () => {
  isMenuOpen.value = false;
});

onMounted(() => {
  if (process.client) {
    const savedTheme = localStorage.getItem('theme');
    if (savedTheme === 'dark' || (!savedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
      isDarkMode.value = true;
      document.documentElement.classList.add('dark');
    } else {
      isDarkMode.value = false;
      document.documentElement.classList.remove('dark');
    }
  }
});
</script>
