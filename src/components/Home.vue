<script setup>
import { ref, onMounted } from 'vue';

const isVisible = ref(false);
const services = ref([
  'Web Development',
  'UI/UX Design',
  'Mobile Apps',
  'Digital Marketing'
]);
const currentService = ref(0);

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        isVisible.value = true;
        setInterval(() => {
          currentService.value = (currentService.value + 1) % services.value.length;
        }, 3000);
        observer.unobserve(entry.target);
      }
    });
  });
  
  observer.observe(document.querySelector('.services-section'));
});
</script>

<template>

  <section class="services-section relative max-w-7xl mx-auto px-6 min-h-screen text-white overflow-hidden">
    
    <div class="relative z-10 flex justify-between flex-wrap items-center gap-12 mt-16 sm:mt-52">
      <!-- Left content -->
      <div 
        class="space-y-8 flex-1"
        :class="{ 'opacity-0 translate-y-8': !isVisible, 'opacity-100 translate-y-0': isVisible }"
        style="transition: all 0.8s ease-out 0.4s"
      >
        <div class="space-y-4">
          <h3 class="text-yellow-500 text-xl font-medium tracking-wide">We Are</h3>
          <h1 class="font-black text-6xl md:text-7xl bg-gradient-to-r from-white to-gray-300 bg-clip-text">
            Company Freelancers
          </h1>
          <div class="h-2 w-24 bg-yellow-500 rounded-full"></div>
        </div>
        
        <p class="text-gray-300 text-lg leading-relaxed sm:max-w-xl">
          We are a team of freelancers who deliver customized web development, design, and digital solutions that turn ideas into impactful products. Let's bring your vision to life with quality and creativity.
        </p>

        <button class="px-8 py-4 bg-yellow-500 hover:bg-yellow-400 text-gray-900 font-semibold rounded-full transition-colors duration-200 transform hover:scale-105">
          Get Started
        </button>
      </div>

      <div 
        class="space-y-4"
        :class="{ 'opacity-0 translate-y-4': !isVisible, 'opacity-100 translate-y-0': isVisible }"
        style="transition: all 0.8s ease-out 0.6s"
      >
        <h2 class="text-4xl font-bold text-yellow-500">Our Services</h2>
        <div class="h-40">
          <transition-group name="fade">
            <p 
              v-for="(service, index) in services" 
              :key="service"
              v-show="currentService === index"
              class="absolute text-2xl space-x-2 text-gray-300 font-medium animate__animated animate__fadeIn"
            >
              <i v-if="service == 'Web Development'" class="fa-solid fa-code"></i>
              <i v-else-if="service == 'Mobile Apps'" class="fa-solid fa-mobile"></i>
              <span>{{ service }}</span>
            </p>
          </transition-group>
        </div>
      </div>
      
    </div>

  </section>

</template>

<style scoped>

.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.fade-enter-to,
.fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}

</style>