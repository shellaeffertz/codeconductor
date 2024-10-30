<script setup>
import { ref, onMounted } from 'vue';

const aboutPoints = ref([
  {
    title: 'Our Mission',
    description: 'Deliver innovative digital solutions that empower businesses to excel.',
  },
  {
    title: 'Our Values',
    description: 'Creativity, dedication, and client satisfaction drive our work forward.',
  },
  {
    title: 'Our Vision',
    description: 'To be the go-to tech partner for transformative digital growth.',
  },
]);

const isAboutVisible = ref(false);

// Particle animations
const particles = ref([]);
const particleCount = 30;

const createParticle = () => ({
  x: Math.random() * window.innerWidth,
  y: Math.random() * window.innerHeight,
  size: Math.random() * 3 + 1,
  speedX: (Math.random() - 0.5) * 2,
  speedY: (Math.random() - 0.5) * 2,
  opacity: Math.random() * 0.5 + 0.3,
});

const initParticles = () => {
  particles.value = Array.from({ length: particleCount }, createParticle);
};

const updateParticles = () => {
  particles.value = particles.value.map(particle => {
    particle.x += particle.speedX;
    particle.y += particle.speedY;
    if (particle.x > window.innerWidth) particle.x = 0;
    if (particle.x < 0) particle.x = window.innerWidth;
    if (particle.y > window.innerHeight) particle.y = 0;
    if (particle.y < 0) particle.y = window.innerHeight;
    return particle;
  });
};

const animateParticles = () => {
  updateParticles();
  requestAnimationFrame(animateParticles);
};

onMounted(() => {
  initParticles();
  animateParticles();
});
</script>

<template>
  <section class="relative max-w-7xl mx-auto px-6 min-h-screen text-white overflow-hidden py-24">
    
    <div class="relative z-10 space-y-16">
      <!-- Header -->
      <div class="text-center space-y-4 animate-on-scroll">
        <h3 class="text-yellow-500 text-xl font-medium tracking-wide">Who We Are</h3>
        <h2 class="font-black text-5xl md:text-6xl bg-gradient-to-r from-white to-gray-300 bg-clip-text text-transparent">
          About Us
        </h2>
        <div class="h-2 w-24 bg-yellow-500 rounded-full mx-auto animate-pulse"></div>
      </div>

      <!-- About Points -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mt-8">
        <template v-for="(point, index) in aboutPoints" :key="point.title">
          <div
            class="relative bg-gray-800/30 backdrop-blur-sm rounded-2xl p-8 border border-gray-700/50 transition-all duration-300 animate-on-scroll"
            :style="{ transition: `all 0.8s ease-out ${0.2 + index * 0.1}s` }"
          >
            <h3 class="text-2xl font-bold text-white">{{ point.title }}</h3>
            <p class="text-gray-300 leading-relaxed mt-4">{{ point.description }}</p>
            <div
              class="absolute inset-0 bg-gradient-to-r from-yellow-500/0 via-yellow-500/5 to-yellow-500/10 opacity-0 hover:opacity-100 transition-opacity duration-300 rounded-2xl"
            ></div>
          </div>
        </template>
      </div>

      <!-- Call to Action -->
      <div class="text-center">
        <button class="px-8 py-4 bg-yellow-500 hover:bg-yellow-400 text-gray-900 font-semibold rounded-full transition-transform duration-200 transform hover:scale-105">
          Meet Our Team
        </button>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes pulse {
  0%, 100% {
    opacity: 0.6;
  }
  50% {
    opacity: 1;
  }
}

.particle {
  transform-origin: center;
  animation: pulse 4s ease-in-out infinite;
}

.animate-on-scroll {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s ease;
}
.is-visible {
  opacity: 1;
  transform: translateY(0);
}
</style>