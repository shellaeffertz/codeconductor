<script setup>

import { ref, onMounted } from 'vue';
import EndSection from './EndSection.vue';
import SectionHeader from './SectionHeader.vue';

const isVisible = ref(false);
const skills = [
  {
    category: 'Development',
    items: [
      { name: 'PHP', progress: 95, color: '#777BB4' },
      { name: 'JavaScript', progress: 90, color: '#F7DF1E' },
      { name: 'Java', progress: 85, color: '#007396' },
      { name: 'Python', progress: 80, color: '#3776AB' },
      { name: 'React', progress: 88, color: '#61DAFB' },
    ],
  },
  {
    category: 'Design & UI',
    items: [
      { name: 'HTML/CSS', progress: 95, color: '#E34F26' },
      { name: 'Figma', progress: 85, color: '#F24E1E' },
      { name: 'Tailwind CSS', progress: 90, color: '#38B2AC' },
      { name: 'UI/UX Design', progress: 85, color: '#FF61F6' },
    ],
  },
  {
    category: 'Digital Marketing',
    items: [
      { name: 'Google Ads', progress: 90, color: '#4285F4' },
      { name: 'SEO', progress: 85, color: '#34A853' },
      { name: 'Social Media', progress: 88, color: '#1DA1F2' },
      { name: 'Analytics', progress: 85, color: '#E37400' },
    ],
  },
];

const updateProgressBars = () => {
  const bars = document.querySelectorAll('.progress-bar');
  bars.forEach((bar) => {
    bar.style.width = bar.dataset.progress + '%';
  });
};

onMounted(() => {
  const sectionRef = document.querySelector('.skills-section');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        isVisible.value = true;
        setTimeout(updateProgressBars, 500);
      } else {
        isVisible.value = false;
        const bars = document.querySelectorAll('.progress-bar');
        bars.forEach((bar) => {
          bar.style.width = '0%';
        });
      }
    });
  }, { threshold: 0.1 });

  if (sectionRef) observer.observe(sectionRef);
});
</script>

<template>
  <section class="skills-section relative max-w-7xl mx-auto px-6 min-h-screen text-white overflow-hidden py-24">

    <div class="relative z-10 space-y-16">

      <SectionHeader>

        <template #subtitle>
          Our Expertise
        </template>

        <template #title>
          Skills & Technologies
        </template>

        <template #description>
          Leveraging the latest tools and technologies, we bring a diverse skill set to every project, ensuring innovative and tailored solutions that meet your unique needs.
        </template>

      </SectionHeader>

      <!-- Skills Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-12">
        <div
          v-for="(category, categoryIndex) in skills"
          :key="category.category"
          class="space-y-6 transition-all duration-800 ease-out"
          :class="{
            'opacity-0 translate-y-8': !isVisible,
            'opacity-100 translate-y-0': isVisible,
          }"
          :style="`transition-delay: ${0.4 + categoryIndex * 0.2}s;`"
        >
          <div class="bg-gray-800/50 backdrop-blur-sm rounded-2xl p-6 border border-gray-700/50">
            <h3 class="text-2xl font-bold text-white mb-2">
              {{ category.category }}
            </h3>
            <div class="h-1 w-12 bg-yellow-500 rounded-full"></div>
          </div>

          <div class="bg-gray-800/50 backdrop-blur-sm rounded-2xl p-6 border border-gray-700/50 space-y-6">
            <div
              v-for="skill in category.items"
              :key="skill.name"
              class="space-y-2"
            >
              <div class="flex justify-between items-center">
                <span class="font-medium">{{ skill.name }}</span>
                <span class="text-sm" :style="{ color: skill.color }">
                  {{ skill.progress }}%
                </span>
              </div>

              <div class="h-2 bg-gray-700 rounded-full overflow-hidden">
                <div
                  class="progress-bar h-full rounded-full transition-all duration-1000 ease-out"
                  :style="{
                    backgroundColor: skill.color,
                    width: '0%',
                  }"
                  :data-progress="skill.progress"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <EndSection>

        <template #title>
          Looking for specific technical expertise?
        </template>

        <template #description>
          Explore how our specialized knowledge can bring your vision to life. We're ready to collaborate and deliver the expertise your project deserves.
        </template>

        <template #btn-label>
          Let's Discuss Your Project
        </template>

      </EndSection>

    </div>
  </section>
</template>

<style scoped>

.progress-bar {
  transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.is-visible {
  opacity: 1;
  transform: translateY(0);
}

</style>
