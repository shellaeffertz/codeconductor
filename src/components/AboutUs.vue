<script setup>

import { ref, onMounted } from 'vue';
import EndSection from './EndSection.vue';
import SectionHeader from './SectionHeader.vue';

const team = ref([
  {
    name: 'Sarah Chen',
    role: 'Lead Developer',
    specialty: 'Full-Stack Development',
    experience: '8+ years',
    image: 'https://mighty.tools/mockmind-api/content/human/7.jpg',
  },
  {
    name: 'Mark Rodriguez',
    role: 'UI/UX Designer',
    specialty: 'User Experience',
    experience: '6+ years',
    image: 'https://mighty.tools/mockmind-api/content/human/60.jpg',
  },
  {
    name: 'Alex Kim',
    role: 'Backend Specialist',
    specialty: 'System Architecture',
    experience: '7+ years',
    image: 'https://mighty.tools/mockmind-api/content/human/41.jpg',
  },
  {
    name: 'Maya Patel',
    role: 'Frontend Expert',
    specialty: 'Modern Frameworks',
    experience: '5+ years',
    image: 'https://mighty.tools/mockmind-api/content/human/42.jpg',
  },
]);

const stats = ref([
  {
    value: '50+',
    label: 'Projects Completed',
  },
  {
    value: '95%',
    label: 'Client Satisfaction',
  },
  {
    value: '6+',
    label: 'Years Experience',
  },
  {
    value: '24/7',
    label: 'Support Available',
  },
]);

const observeElements = (elements) => {
  const options = {
    root: null,
    threshold: 0.1,
  };

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
      }
    });
  }, options);

  elements.forEach((element) => observer.observe(element));
};

onMounted(() => {
  const animatedElements = document.querySelectorAll('.animate-on-scroll');
  observeElements(animatedElements);
});
</script>

<template>
  <section class="relative max-w-7xl mx-auto px-6 min-h-screen text-white overflow-hidden py-24">
    <div class="relative z-10 space-y-16">

      <SectionHeader>

        <template #subtitle>
          About Us
        </template>

        <template #title>
          Passionate About<br />Technology
        </template>

        <template #description>
          We're a dynamic team of developers, designers, and digital craftsmen dedicated to turning your vision into exceptional digital experiences.
        </template>

      </SectionHeader>

      <!-- Stats Grid -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-8 animate-on-scroll" style="transition: all 0.8s ease-out 0.4s">
        <div v-for="stat in stats" :key="stat.label" class="text-center space-y-2">
          <p class="text-4xl font-bold text-yellow-500">{{ stat.value }}</p>
          <p class="text-gray-300">{{ stat.label }}</p>
        </div>
      </div>

      <!-- Team Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
        <div
          v-for="(member, index) in team"
          :key="member.name"
          class="group relative bg-gray-800/30 backdrop-blur-sm rounded-2xl p-6 border border-gray-700/50 hover:border-yellow-500/50 transition-all duration-300 animate-on-scroll"
          :style="`transition: all 0.8s ease-out ${0.6 + index * 0.2}s`"
        >
          <div class="space-y-4">
            <img 
              :src="member.image" 
              :alt="member.name"
              class="w-24 h-24 rounded-full mx-auto object-cover border-2 border-yellow-500"
            />
            <div class="text-center">
              <h3 class="text-xl font-bold text-white group-hover:text-yellow-500 transition-colors duration-300">
                {{ member.name }}
              </h3>
              <p class="text-yellow-500 font-medium">{{ member.role }}</p>
              <p class="text-gray-300 text-sm mt-2">{{ member.specialty }}</p>
              <p class="text-gray-400 text-sm">{{ member.experience }}</p>
            </div>
          </div>

          <!-- Hover Effect -->
          <div
            class="absolute inset-0 bg-gradient-to-r from-yellow-500/0 via-yellow-500/5 to-yellow-500/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-2xl"
          ></div>
        </div>
      </div>

      <EndSection>

        <template #title>
          Our Mission
        </template>

        <template #description>
          To deliver cutting-edge solutions that empower businesses to thrive in the digital age. We combine technical excellence with creative innovation to create lasting value for our clients.
        </template>

        <template #btn-label>
          Meet Our Team
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