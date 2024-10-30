<script setup>
import { ref, onMounted } from 'vue';

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
      <!-- Header -->
      <div
        class="text-center space-y-4 transition-all duration-800 ease-out delay-200"
        :class="{ 'opacity-0 translate-y-8': !isVisible, 'opacity-100 translate-y-0': isVisible }"
      >
        <h3 class="text-yellow-500 text-xl font-medium tracking-wide animate-pop-in">
          Our Expertise
        </h3>
        <h2 class="font-black text-5xl md:text-6xl bg-gradient-to-r from-white to-gray-300 bg-clip-text">
          Skills & Technologies
        </h2>
        <div class="h-2 w-24 bg-yellow-500 rounded-full mx-auto animate-pulse-fast"></div>
      </div>

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

      <div
        class="text-center space-y-6 transition-all duration-800 ease-out delay-800"
        :class="{ 'opacity-0 translate-y-8': !isVisible, 'opacity-100 translate-y-0': isVisible }"
      >
        <p class="text-gray-300 text-lg">
          Looking for specific technical expertise?
        </p>
        <button class="px-8 py-4 bg-yellow-500 hover:bg-yellow-400 text-gray-900 font-semibold rounded-full transition-colors duration-200">
          Let's Discuss Your Project
        </button>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes float {
  0%, 100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-10px) scale(1.05);
  }
}

.progress-bar {
  transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes pop-in {
  from {
    transform: scale(0.8);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

.animate-pop-in {
  animation: pop-in 0.8s ease forwards;
}

@keyframes pulse-slow {
  0%, 100% {
    opacity: 0.6;
  }
  50% {
    opacity: 1;
  }
}

.animate-pulse-fast {
  animation: pulse-slow 1s ease-in-out infinite;
}
</style>
