<script setup>
import { ref } from "vue";

const isMenuOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};
</script>

<template>
  <nav
    class="relative z-50 max-w-7xl mx-auto px-6 py-3 flex items-center text-white"
  >
    <div class="flex-1 flex items-center gap-28">
      <div class="flex-shrink-0 flex items-center">
        <a href="#" class="flex items-center group">
          <div
            class="logo-icon w-9 h-9 bg-white rounded-full shadow-lg flex items-center justify-center transform transition-transform duration-300 group-hover:rotate-12 group-hover:scale-125"
          >
            <i class="fa-solid fa-dove text-xl text-yellow-600"></i>
          </div>
          <span
            class="ml-3 text-white font-bold text-xl transform transition-transform duration-300 group-hover:translate-x-1"
          >
            Portfolio
          </span>
        </a>
      </div>

      <ul class="hidden md:flex items-center gap-4 text-white">
        <li>
          <a class="hover:text-gray-400 transition-colors" href="#">Home</a>
        </li>
        <li>
          <a class="hover:text-gray-400 transition-colors" href="#">About</a>
        </li>
        <li>
          <a class="hover:text-gray-400 transition-colors" href="#">Projects</a>
        </li>
        <li>
          <a class="hover:text-gray-400 transition-colors" href="#">Contact</a>
        </li>
      </ul>
    </div>

    <ul class="shrink-0 flex items-center gap-4 text-white">
      <li>
        <a
          class="block duration-150 hover:text-yellow-600 hover:scale-125 hover:rotate-12"
          href="#"
        >
          <i class="fab fa-linkedin text-2xl"></i>
        </a>
      </li>
      <li>
        <a
          class="block duration-150 hover:text-yellow-600 hover:scale-125 hover:rotate-12"
          href="#"
        >
          <i class="fab fa-github text-2xl"></i>
        </a>
      </li>
      <li>
        <button
          class="md:hidden group space-y-1 w-7 focus:outline-none"
          @click="toggleMenu"
        >
          <span
            class="block duration-150 h-0.5 w-full bg-white group-hover:bg-yellow-600"
          ></span>
          <span
            class="block duration-150 h-0.5 bg-white group-hover:bg-yellow-600"
            :class="{ 'w-1/2': !isMenuOpen, 'w-full': isMenuOpen }"
          ></span>
          <span
            class="block duration-150 h-0.5 w-full bg-white group-hover:bg-yellow-600"
          ></span>
        </button>
      </li>
    </ul>
  </nav>

  <div
    class="md:hidden relative top-[calc(100%+5px)] left-0 w-full px-4 bg-gray-900 space-y-2 min text-white duration-150 overflow-hidden"
    :class="{'h-0': !isMenuOpen, 'py-4 h-fit': isMenuOpen}"
  >
    <a href="#" class="block hover:text-yellow-600 transition-colors">
      <i class="fa-solid fa-house mr-2"></i>
      <span>Home</span>
    </a>
    <a href="#" class="block hover:text-yellow-600 transition-colors">
      <i class="fa-solid fa-user mr-2"></i>
      <span>About</span>
    </a>
    <a href="#" class="block hover:text-yellow-600 transition-colors">
      <i class="fa-solid fa-briefcase mr-2"></i>
      <span>Projects</span>
    </a>
    <a href="#" class="block hover:text-yellow-600 transition-colors">
      <i class="fa-solid fa-envelope mr-2"></i>
      <span>Contact</span>
    </a>
  </div>
</template>
