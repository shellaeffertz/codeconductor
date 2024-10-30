<script setup>

import { onMounted } from 'vue';

onMounted(() => {
  const elements = document.querySelectorAll('.opacity-0');
  elements.forEach((el, index) => {
    el.classList.remove('opacity-0');
    el.classList.add('opacity-100');
    el.style.transform = 'translate-y-0';
  });
});

</script>

<template>
  <footer class="bg-gray-900 pb-24 pt-8 relative text-gray-400"> 
    <div class="max-w-7xl mx-auto px-6 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-10">
      
      <!-- Zewana Info & Social Links -->
      <div class="space-y-6 opacity-0 transform translate-y-8 transition-all duration-700">
        <div class="flex items-center">
          <a href="#" class="flex items-center group">
            <div
              class="logo-icon w-14 h-14 bg-white rounded-full shadow-lg flex items-center justify-center transform transition-transform duration-300 group-hover:rotate-12 group-hover:scale-125"
            >
              <i class="fa-solid fa-dove text-xl text-yellow-600"></i>
            </div>
            <span
              class="ml-3 text-white font-bold text-3xl transform transition-transform duration-300 group-hover:translate-x-1"
            >
              Portfolio
            </span>
          </a>
        </div>
        <ul class="flex gap-4">
          <li>
            <a href="#" class="w-12 h-12 flex items-center justify-center bg-gray-700 rounded-full duration-150 hover:bg-blue-600 hover:text-white hover:scale-105 hover:rotate-12">
              <i class="fab fa-facebook-f text-2xl"></i>
            </a>
          </li>
          <li>
            <a href="#" class="w-12 h-12 flex items-center justify-center bg-gray-700 rounded-full duration-150 hover:bg-black hover:text-white hover:scale-105 hover:rotate-12">
              <i class="fa-brands fa-x-twitter"></i>
            </a>
          </li>
          <li>
            <a href="#" class="w-12 h-12 flex items-center justify-center bg-gray-700 rounded-full duration-150 hover:bg-red-600 hover:text-white hover:scale-105 hover:rotate-12">
              <i class="fab fa-youtube text-2xl"></i>
            </a>
          </li>
        </ul>
        <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Temporibus nulla rem, dignissimos iste aspernatur.</p>
      </div>

      <!-- Important Links -->
      <div class="opacity-0 transform translate-y-8 transition-all duration-700 delay-200">
        <h3 class="text-yellow-500 font-bold mb-4">Quick Links</h3>
        <ul class="space-y-4">
          <li class="hover:translate-x-1 duration-300">
            <a href="#" class="block hover:text-yellow-500 space-x-2">
              <i class="fa-solid fa-angles-right"></i>
              <span>Home</span>
            </a>
          </li>
          <li class="hover:translate-x-1 duration-300">
            <a href="#" class="block hover:text-yellow-500 space-x-2">
              <i class="fa-solid fa-angles-right"></i>
              <span>About Us</span>
            </a>
          </li>
          <li class="hover:translate-x-1 duration-300">
            <a href="#" class="block hover:text-yellow-500 space-x-2">
              <i class="fa-solid fa-angles-right"></i>
              <span>Services</span>
            </a>
          </li>
          <li class="hover:translate-x-1 duration-300">
            <a href="#" class="block hover:text-yellow-500 space-x-2">
              <i class="fa-solid fa-angles-right"></i>
              <span>Projects</span>
            </a>
          </li>
          <li class="hover:translate-x-1 duration-300">
            <a href="#" class="block hover:text-yellow-500 space-x-2">
              <i class="fa-solid fa-angles-right"></i>
              <span>Skills</span>
            </a>
          </li>
        </ul>
      </div>

      <!-- Contact Information -->
      <div class="space-y-6 opacity-0 transform translate-y-8 transition-all duration-700 delay-400">
        <h3 class="text-yellow-500 font-bold mb-4">Contact Information</h3>
        <div class="flex items-center space-x-4">
          <i class="fas fa-map-marker-alt text-yellow-500 text-2xl"></i>
          <div>Egypt, Giza, Inside The Sphinx, Room Number 220</div>
        </div>
        <div class="flex items-center space-x-4">
          <i class="far fa-clock text-yellow-500 text-2xl"></i>
          <div>Business Hours: From 10:00 To 18:00</div>
        </div>
        <div class="flex items-center space-x-4">
          <i class="fas fa-phone-volume text-yellow-500 text-2xl"></i>
          <div>
            <p>+20123456789</p>
            <p>+20198765432</p>
          </div>
        </div>
      </div> 

      <!-- Gallery -->
      <div class="opacity-0 transform translate-y-8 transition-all duration-700 delay-600">
        <h3 class="text-yellow-500 font-bold mb-4">Projects</h3>
        <div class="flex flex-wrap gap-4">
          <img src="https://cdn2.hubspot.net/hubfs/53/mint-homepage-design.png" alt="Gallery 1" class="w-1/3 border-2 border-white transform transition-transform duration-300 hover:scale-110 hover:rotate-3">
          <img src="https://www.searchenginejournal.com/wp-content/uploads/2019/10/titan-storage-solutions-home-page-example-5dbbef237e7e3.jpg" alt="Gallery 2" class="w-1/3 border-2 border-white transform transition-transform duration-300 hover:scale-110 hover:rotate-3">
          <img src="https://knowledge.hubspot.com/hs-fs/hubfs/Telerik.webp?width=650&height=409&name=Telerik.webp" alt="Gallery 3" class="w-1/3 border-2 border-white transform transition-transform duration-300 hover:scale-110 hover:rotate-3">
          <img src="https://miro.medium.com/v2/resize:fit:850/1*g11qQ2nRu4haeft4X648cQ.jpeg" alt="Gallery 4" class="w-1/3 border-2 border-white transform transition-transform duration-300 hover:scale-110 hover:rotate-3">
        </div>
      </div>

    </div>

    <p class="bg-gray-900 absolute bottom-0 left-0 w-full text-center py-4 border-t border-gray-700 text-gray-400 opacity-0 transform translate-y-8 transition-all duration-700 delay-800">
      Made With &lt;3 By Me
    </p>
  </footer>
</template>

<style scoped>
/* Scoped styles if necessary */
</style>