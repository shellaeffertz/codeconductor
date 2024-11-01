<script setup>

import { ref, onMounted } from 'vue';
import EndSection from './EndSection.vue';
import SectionHeader from './SectionHeader.vue';

const isVisible = ref(false);
const currentProject = ref(0);
const direction = ref('next');

const projects = ref([
  {
    title: 'TechFlow Dashboard',
    category: 'Web Application',
    technologies: ['React', 'Node.js', 'MongoDB', 'Tailwind CSS'],
    description: 'A comprehensive analytics dashboard that processes real-time data for enterprise clients. Features include customizable widgets, data visualization, and automated reporting.',
    image: 'https://cdn2.hubspot.net/hubfs/53/mint-homepage-design.png',
    stats: {
      users: '50K+',
      dataPoints: '2M+',
      uptime: '99.9%'
    },
    links: {
      live: '#',
      github: '#'
    }
  },
  {
    title: 'EcoTrack Mobile',
    category: 'Mobile App',
    technologies: ['React Native', 'Firebase', 'Redux', 'Google Maps API'],
    description: 'An eco-friendly transportation tracker that helps users reduce their carbon footprint through smart route planning and sustainable travel recommendations.',
    image: 'https://www.searchenginejournal.com/wp-content/uploads/2019/10/titan-storage-solutions-home-page-example-5dbbef237e7e3.jpg',
    stats: {
      downloads: '100K+',
      carbonSaved: '500T',
      activeUsers: '25K'
    },
    links: {
      appStore: '#',
      playStore: '#'
    }
  },
  {
    title: 'SmartHome Hub',
    category: 'IoT Platform',
    technologies: ['Vue.js', 'Python', 'AWS', 'WebSocket'],
    description: 'A centralized IoT platform for smart home device management, featuring real-time control, automation schedules, and energy consumption analytics.',
    image: 'https://knowledge.hubspot.com/hs-fs/hubfs/Telerik.webp?width=650&height=409&name=Telerik.webp',
    stats: {
      devices: '1M+',
      automations: '5M+',
      reliability: '99.99%'
    },
    links: {
      live: '#',
      docs: '#'
    }
  }
]);

onMounted(() => {
  const sectionRef = document.querySelector('.portfolio-section');
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        isVisible.value = entry.isIntersecting;
      });
    },
    { threshold: 0.1 }
  );

  if (sectionRef) observer.observe(sectionRef);
  startAutoPlay();
});

const startAutoPlay = () => {
  setInterval(() => {
    goToNext();
  }, 6000);
};

const goToProject = (index) => {
  direction.value = index > currentProject.value ? 'next' : 'prev';
  currentProject.value = index;
};

const goToNext = () => {
  direction.value = 'next';
  currentProject.value = (currentProject.value + 1) % projects.value.length;
};

const goToPrev = () => {
  direction.value = 'prev';
  currentProject.value = currentProject.value === 0 
    ? projects.value.length - 1 
    : currentProject.value - 1;
};
</script>

<template>
  <section class="portfolio-section relative max-w-7xl mx-auto px-6 min-h-[90vh] text-white overflow-hidden py-24">
    <div class="relative z-10 space-y-16">
      
      <SectionHeader>

        <template #subtitle>
          Our Portfolio
        </template>

        <template #title>
          Featured Projects
        </template>

        <template #description>
          Discover a showcase of our standout projects, where innovation and expertise come together to create impactful digital solutions tailored to our clients' goals.
        </template>

      </SectionHeader>


      <!-- Projects Carousel -->
      <div
        class="max-w-6xl mx-auto"
        :class="{ 'opacity-0 translate-y-8': !isVisible, 'opacity-100 translate-y-0': isVisible }"
        style="transition: all 1.2s ease-out 0.4s"
      >
        <div class="relative h-[600px] overflow-hidden">
          <!-- Navigation Arrows -->
          <button 
            @click="goToPrev" 
            class="absolute left-3 top-1/2 -translate-y-1/2 z-10 bg-gray-800/50 hover:bg-gray-700/50 p-4 rounded-full transform -translate-x-1/2 transition-all duration-300"
          >
            ←
          </button>
          <button 
            @click="goToNext" 
            class="absolute right-3 top-1/2 -translate-y-1/2 z-10 bg-gray-800/50 hover:bg-gray-700/50 p-4 rounded-full transform translate-x-1/2 transition-all duration-300"
          >
            →
          </button>

          <!-- Projects -->
          <div class="relative w-full h-full">
            <transition-group 
              :name="direction === 'next' ? 'slide-next' : 'slide-prev'"
              tag="div"
              class="relative w-full h-full"
            >
              <div
                v-for="(project, index) in projects"
                :key="project.title"
                v-show="currentProject === index"
                class="absolute inset-0 w-full"
              >
                <div class="bg-gray-800/50 backdrop-blur-sm rounded-2xl p-8 border border-gray-700/50 h-full">
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-8 h-full">
                    <!-- Project Image -->
                    <div class="relative group overflow-hidden rounded-xl hidden md:block">
                      <img
                        :src="project.image"
                        :alt="project.title"
                        class="w-full h-full object-cover transform group-hover:scale-110 transition-transform duration-500"
                      />
                      <div class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                        <div class="absolute bottom-0 left-0 right-0 p-6 space-y-2">
                          <div class="flex gap-4">
                            <a v-for="(link, key) in project.links" 
                               :key="key"
                               :href="link"
                               class="px-4 py-2 text-gray-900 bg-yellow-500 hover:bg-yellow-400 rounded-full text-sm font-medium transition-colors duration-200">
                              {{ key.charAt(0).toUpperCase() + key.slice(1) }}
                            </a>
                          </div>
                        </div>
                      </div>
                    </div>

                    <!-- Project Details -->
                    <div class="flex flex-col justify-between">
                      <div class="space-y-6">
                        <div>
                          <p class="text-yellow-500 text-sm font-medium mb-2">{{ project.category }}</p>
                          <h3 class="text-3xl font-bold">{{ project.title }}</h3>
                        </div>
                        <p class="text-gray-300 leading-relaxed">{{ project.description }}</p>
                        <div class="flex flex-wrap gap-2">
                          <span 
                            v-for="tech in project.technologies" 
                            :key="tech"
                            class="px-3 py-1 bg-gray-700/50 rounded-full text-sm text-yellow-300"
                          >
                            {{ tech }}
                          </span>
                        </div>
                      </div>

                      <!-- Project Stats -->
                      <div class="grid grid-cols-3 gap-4 mt-8">
                        <div 
                          v-for="(value, key) in project.stats" 
                          :key="key"
                          class="text-center py-4 bg-gray-700/30 rounded-lg"
                        >
                          <p class="text-xl sm:text-2xl font-bold text-yellow-500">{{ value }}</p>
                          <p class="text-xs sm:text-sm text-gray-400 text-center">{{ key.replace(/([A-Z])/g, ' $1').trim() }}</p>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </transition-group>
          </div>
        </div>
      </div>
    

      <EndSection>

        <template #title>
          Interested in working with us?
        </template>

        <template #description>
          We’re excited to collaborate and bring your ideas to life. Let’s connect and explore how we can create extraordinary solutions together.
        </template>

        <template #btn-label>
          Let's Build Something Amazing
        </template>

      </EndSection>

    </div>
  </section>
</template>

<style scoped>

.slide-next-enter-active,
.slide-next-leave-active,
.slide-prev-enter-active,
.slide-prev-leave-active {
  transition: all 0.5s ease-in-out;
  position: absolute;
  width: 100%;
}

.slide-next-enter-from {
  transform: translateX(100%);
  opacity: 0;
}

.slide-next-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}

.slide-prev-enter-from {
  transform: translateX(-100%);
  opacity: 0;
}

.slide-prev-leave-to {
  transform: translateX(100%);
  opacity: 0;
}

.slide-next-enter-active,
.slide-prev-enter-active {
  z-index: 1;
}

.is-visible {
  opacity: 1;
  transform: translateY(0);
}
</style>