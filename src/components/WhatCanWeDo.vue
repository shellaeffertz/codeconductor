<script setup>

import { ref, onMounted } from 'vue';
import EndSection from './EndSection.vue';
import SectionHeader from './SectionHeader.vue';

const capabilities = ref([
  {
    title: 'Custom Development',
    description: 'Tailored solutions built from scratch to meet your specific business needs and requirements.',
    stats: '100+ Projects Delivered',
  },
  {
    title: 'Modern Design',
    description: 'Stunning, responsive designs that work seamlessly across all devices and platforms.',
    stats: '50+ Happy Clients',
  },
  {
    title: 'Fast Delivery',
    description: 'Quick turnaround times without compromising on quality or attention to detail.',
    stats: '2 Weeks Average',
  },
  {
    title: 'Ongoing Support',
    description: 'Dedicated maintenance and support to ensure your solution continues to evolve and perform.',
    stats: '24/7 Support',
  },
]);

// New particle system setup
const particles = ref([]);
const particleCount = 50;

const createParticle = () => ({
  x: Math.random() * window.innerWidth,
  y: Math.random() * window.innerHeight,
  size: Math.random() * 3 + 1,
  speedX: (Math.random() - 0.5) * 2,
  speedY: (Math.random() - 0.5) * 2,
  opacity: Math.random() * 0.5 + 0.3,
  hue: Math.random() * 60 + 30, // Golden hues (30-90)
});

const initParticles = () => {
  particles.value = Array.from({ length: particleCount }, createParticle);
};

const updateParticles = () => {
  particles.value = particles.value.map(particle => {
    particle.x += particle.speedX;
    particle.y += particle.speedY;

    // Wrap particles around screen
    if (particle.x > window.innerWidth) particle.x = 0;
    if (particle.x < 0) particle.x = window.innerWidth;
    if (particle.y > window.innerHeight) particle.y = 0;
    if (particle.y < 0) particle.y = window.innerHeight;

    return particle;
  });
};

const animate = () => {
  updateParticles();
  requestAnimationFrame(animate);
};

const observeElements = (elements) => {
  const options = {
    root: null,
    threshold: 0.1,
  };

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
      } else {
        entry.target.classList.remove('is-visible');
      }
    });
  }, options);

  elements.forEach((element) => observer.observe(element));
};

onMounted(() => {
  const animatedElements = document.querySelectorAll('.animate-on-scroll');
  observeElements(animatedElements);
  
  initParticles();
  animate();
});
</script>

<template>
  <section class="relative max-w-7xl mx-auto px-6 min-h-screen text-white overflow-hidden py-24">

    <div class="relative z-10 space-y-16">

      <SectionHeader>

        <template #subtitle>
          What We Do
        </template>

        <template #title>
          Transforming Ideas<br />Into Reality
        </template>

        <template #description>
          We specialize in bringing ideas to life through innovative digital solutions. From design to development, our team combines creativity and technical skill to build experiences that captivate and connect.
        </template>

      </SectionHeader>


      <!-- Capabilities Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <template v-for="(capability, index) in capabilities" :key="capability.title">
          <div
            class="group relative bg-gray-800/30 backdrop-blur-sm rounded-2xl p-8 border border-gray-700/50 hover:border-yellow-500/50 transition-all duration-300 animate-on-scroll"
            :style="`transition: all 0.8s ease-out ${0.4 + index * 0.2}s`"
          >
            <div class="space-y-4">
              <h3 class="text-2xl font-bold text-white group-hover:text-yellow-500 transition-colors duration-300">
                {{ capability.title }}
              </h3>
              <p class="text-gray-300 leading-relaxed">
                {{ capability.description }}
              </p>
              <div class="pt-4 border-t border-gray-700/50">
                <p class="text-yellow-500 font-semibold">{{ capability.stats }}</p>
              </div>
            </div>

            <!-- Hover Effect -->
            <div
              class="absolute inset-0 bg-gradient-to-r from-yellow-500/0 via-yellow-500/5 to-yellow-500/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-2xl"
            ></div>
          </div>
        </template>
      </div>

     <EndSection>

      <template #title>
        Why Partner With Us
      </template>

      <template #description>
        We’re driven to craft solutions that elevate your business in the digital landscape. Blending innovation with expertise, we create impactful results that last.
      </template>

      <template #btn-label>
        Let’s Collaborate
      </template>

     </EndSection>

    </div>
  </section>
</template>

<style scoped>

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