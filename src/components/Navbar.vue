<script setup>

import Logo from "./Logo.vue";
import { ref, onMounted, onUnmounted } from "vue";

const isMenuOpen = ref(false);
const isScrolled = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});

const menuItems = [
  { 
    label: 'Home', 
    icon: 'fa-solid fa-house',
    href: '#home'
  },
  { 
    label: 'About Us', 
    icon: 'fa-solid fa-user',
    href: '#about-us'
  },
  { 
    label: 'Services', 
    icon: 'fa-solid fa-gears',
    href: '#services'
  },
  { 
    label: 'Projects', 
    icon: 'fa-solid fa-briefcase',
    href: '#projects'
  },
  { 
    label: 'Contact', 
    icon: 'fa-solid fa-envelope',
    href: '#contact'
  }
];

const socialLinks = [
  { 
    icon: 'fab fa-linkedin', 
    href: 'https://linkedin.com'
  },
  { 
    icon: 'fab fa-github', 
    href: 'https://github.com'
  }
];
</script>

<template>
  <nav 
    class="fixed top-0 left-0 right-0 z-[99998] transition-all duration-300"
    :class="{
      'bg-gray-900/80 backdrop-blur-md shadow-lg': isScrolled,
      'bg-transparent': !isScrolled
    }"
  >
    <!-- Existing desktop navigation code remains the same -->

    <div class="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between text-white">
      <!-- Logo -->
      <div class="flex-shrink-0">
        <a href="#" class="flex items-center group">
          <div 
            class="logo-icon transform transition-transform duration-300 group-hover:rotate-12 group-hover:scale-125"
          >
            <Logo class="w-16 aspect-square" />
          </div>
        </a>
      </div>

      <!-- Desktop Navigation -->
      <ul class="hidden md:flex items-center gap-6 text-white">
        <li 
          v-for="item in menuItems" 
          :key="item.label" 
          class="group relative"
        >
          <a 
            :href="item.href"
            class="flex items-center gap-2 hover:text-yellow-500 transition-colors duration-300 group-hover:scale-105"
          >
            <i :class="item.icon" class="transition-transform duration-300"></i>
            {{ item.label }}
            <span 
              class="absolute bottom-[-4px] left-0 w-0 h-0.5 bg-yellow-500 transition-all duration-300 group-hover:w-full"
            ></span>
          </a>
        </li>
      </ul>

      <!-- Social and Mobile Menu Toggle -->
      <div class="flex items-center gap-4">
        <!-- Social Links -->
        <ul class="flex items-center gap-3">
          <li 
            v-for="link in socialLinks" 
            :key="link.icon"
          >
            <a 
              :href="link.href" 
              target="_blank"
              class="block duration-150 hover:text-yellow-600 hover:scale-125 hover:rotate-12"
            >
              <i :class="[link.icon, 'text-2xl hover:text-yellow-500']"></i>
            </a>
          </li>
        </ul>

        <!-- Mobile Menu Toggle -->
        <button
          class="md:hidden group space-y-1.5 w-8 focus:outline-none"
          @click="toggleMenu"
        >
          <span 
            class="block duration-300 h-0.5 w-full bg-white origin-left"
            :class="{
              'rotate-45 translate-x-1 translate-y-1': isMenuOpen,
              'rotate-0': !isMenuOpen
            }"
          ></span>
          <span 
            class="block duration-300 h-0.5 bg-white"
            :class="{
              'w-0 opacity-0': isMenuOpen,
              'w-full opacity-100': !isMenuOpen
            }"
          ></span>
          <span 
            class="block duration-300 h-0.5 w-full bg-white origin-left"
            :class="{
              '-rotate-45 translate-x-1 -translate-y-1': isMenuOpen,
              'rotate-0': !isMenuOpen
            }"
          ></span>
        </button>
      </div>
    </div>
  </nav>

  <!-- Mobile Menu -->
  <div 
      class="md:hidden fixed top-0 left-0 w-full h-full bg-gray-900 z-[100000] transform transition-transform duration-300 ease-in-out overflow-hidden"
      :class="{
        'translate-x-full': !isMenuOpen,
        'translate-x-0': isMenuOpen
      }"
    >
      <!-- Close Button -->
      <button 
        @click="toggleMenu" 
        class="absolute top-6 right-6 group focus:outline-none"
      >
        <div class="relative w-10 h-10">
          <span 
            class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 block w-6 h-0.5 bg-white rotate-45 transition-all duration-300 group-hover:rotate-[135deg]"
          ></span>
          <span 
            class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 block w-6 h-0.5 bg-white -rotate-45 transition-all duration-300 group-hover:rotate-[225deg]"
          ></span>
        </div>
      </button>

      <div class="flex flex-col h-full pt-24 px-8 space-y-6">
        <a 
          v-for="item in menuItems" 
          :key="item.label"
          :href="item.href"
          @click="toggleMenu"
          class="text-3xl font-bold text-white flex items-center gap-4 transform transition-all duration-300 hover:translate-x-4 hover:text-yellow-500"
        >
          <i :class="item.icon" class="text-2xl w-8"></i>
          {{ item.label }}
        </a>

        <div class="mt-auto pb-12 flex justify-center space-x-6">
          <a 
            v-for="link in socialLinks" 
            :key="link.icon"
            :href="link.href"
            target="_blank"
            class="text-4xl transform transition-all duration-300 hover:scale-125 hover:rotate-12"
          >
            <i :class="link.icon" class="text-white"></i>
          </a>
        </div>
      </div>
    </div>

</template>