<script setup>
import { ref, onMounted } from 'vue';

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
  
  // Initialize particle system
  initParticles();
  animate();
});
</script>

<template>
  <section class="relative max-w-7xl mx-auto px-6 min-h-screen text-white overflow-hidden py-24">

    <div class="relative z-10 space-y-16">
      <!-- Header -->
      <div
        class="text-center space-y-4 animate-on-scroll"
        style="transition: all 0.8s ease-out 0.2s"
      >
        <h3 class="text-yellow-500 text-xl font-medium tracking-wide animate-pop-in">What We Do</h3>
        <h2 class="font-black text-5xl md:text-6xl bg-gradient-to-r from-white to-gray-300 bg-clip-text animate-gradient-pop">
          Transforming Ideas<br />Into Reality
        </h2>
        <div class="h-2 w-24 bg-yellow-500 rounded-full mx-auto animate-pulse-fast"></div>
      </div>

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

      <!-- Call to Action -->
      <div
        class="text-center animate-on-scroll"
        style="transition: all 0.8s ease-out 1s"
      >
        <button class="px-8 py-4 bg-yellow-500 hover:bg-yellow-400 text-gray-900 font-semibold rounded-full transition-colors duration-200 animate-pop-in">
          Start Your Project
        </button>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes float-slow {
  0%, 100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-10px) scale(1.05);
  }
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

@keyframes slide-in {
  from {
    transform: translateY(20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes pulse-slow {
  0%, 100% {
    opacity: 0.6;
  }
  50% {
    opacity: 1;
  }
}

.particle {
  transform-origin: center;
  transition: all 0.3s ease;
}

.animate-float-slow {
  animation: float-slow 6s ease-in-out infinite;
}
.animate-pop-in {
  animation: pop-in 0.8s ease forwards;
}
.animate-slide-in {
  animation: slide-in 1.2s ease forwards;
}
.animate-pulse-slow {
  animation: pulse-slow 4s ease-in-out infinite;
}
.animate-pulse-fast {
  animation: pulse-slow 1s ease-in-out infinite;
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

.bg-gradient-radial {
  background-image: radial-gradient(var(--tw-gradient-stops));
}
</style>