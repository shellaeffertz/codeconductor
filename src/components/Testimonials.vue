<script setup>
import { ref, onMounted } from 'vue';

const isVisible = ref(false);
const currentTestimonial = ref(0);
const testimonials = ref([
  {
    name: 'Sarah Johnson',
    role: 'CEO at TechStart',
    image: 'https://mighty.tools/mockmind-api/content/human/65.jpg',
    content:
      'Working with this team was an absolute game-changer for our startup. Their web development expertise helped us launch our platform months ahead of schedule.',
    rating: 5,
  },
  {
    name: 'Michael Chen',
    role: 'Product Manager',
    image: 'https://mighty.tools/mockmind-api/content/human/44.jpg',
    content:
      'The UI/UX design they delivered exceeded our expectations. Our user engagement has increased by 150% since the redesign.',
    rating: 5,
  },
  {
    name: 'Emma Davis',
    role: 'Founder at MobileFirst',
    image: 'https://mighty.tools/mockmind-api/content/human/68.jpg',
    content:
      'Their mobile app development skills are outstanding. They turned our concept into a polished app that our users love. Highly recommended!',
    rating: 5,
  },
]);

const direction = ref('next'); // Track animation direction

onMounted(() => {
  const sectionRef = document.querySelector('.testimonial-section');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        isVisible.value = true;
      } else {
        isVisible.value = false;
      }
    });
  }, { threshold: 0.1 });

  if (sectionRef) observer.observe(sectionRef);

  startAutoPlay();
});

const startAutoPlay = () => {
  setInterval(() => {
    goToNext();
  }, 5000);
};

const goToTestimonial = (index) => {
  direction.value = index > currentTestimonial.value ? 'next' : 'prev';
  currentTestimonial.value = index;
};

const goToNext = () => {
  direction.value = 'next';
  currentTestimonial.value = (currentTestimonial.value + 1) % testimonials.value.length;
};

const goToPrev = () => {
  direction.value = 'prev';
  currentTestimonial.value = currentTestimonial.value === 0 
    ? testimonials.value.length - 1 
    : currentTestimonial.value - 1;
};
</script>

<template>

  <section class="testimonial-section relative max-w-7xl mx-auto px-6 min-h-[80vh] text-white overflow-hidden py-24">

    <div class="relative z-10 space-y-16">
      <!-- Header -->
      <div
        class="text-center space-y-4"
        :class="{ 'opacity-0 translate-y-8': !isVisible, 'opacity-100 translate-y-0': isVisible }"
        style="transition: all 1s ease-out 0.2s"
      >
        <h3 class="text-yellow-500 text-xl font-medium tracking-wide animate-pop-in">Testimonials</h3>
        <h2 class="font-black text-5xl md:text-6xl bg-gradient-to-r from-white to-gray-300 bg-clip-text animate-gradient-pop">
          What Our Clients Say
        </h2>
        <div class="h-2 w-24 bg-yellow-500 rounded-full mx-auto animate-pulse-fast"></div>
      </div>

      <!-- Testimonials Carousel -->
      <div
        class="max-w-4xl mx-auto"
        :class="{ 'opacity-0 translate-y-8': !isVisible, 'opacity-100 translate-y-0': isVisible }"
        style="transition: all 1.2s ease-out 0.4s"
      >
        <div class="relative h-[400px] overflow-hidden">
          <!-- Navigation Arrows -->
          <button 
            @click="goToPrev" 
            class="absolute left-3 top-1/2 -translate-y-1/2 z-10 bg-gray-800/50 hover:bg-gray-700/50 p-3 rounded-full transform -translate-x-1/2 transition-all duration-300"
          >
            ←
          </button>
          <button 
            @click="goToNext" 
            class="absolute right-3 top-1/2 -translate-y-1/2 z-10 bg-gray-800/50 hover:bg-gray-700/50 p-3 rounded-full transform translate-x-1/2 transition-all duration-300"
          >
            →
          </button>

          <!-- Testimonials -->
          <div class="relative w-full h-full">
            <transition-group 
              :name="direction === 'next' ? 'slide-next' : 'slide-prev'"
              tag="div"
              class="relative w-full h-full"
            >
              <div
                v-for="(testimonial, index) in testimonials"
                :key="testimonial.name"
                v-show="currentTestimonial === index"
                class="absolute inset-0 w-full"
              >
                <div class="bg-gray-800/50 backdrop-blur-sm rounded-2xl p-8 border border-gray-700/50 h-full flex flex-col items-center justify-center text-center">
                  <div class="text-6xl text-yellow-500/20 font-serif mb-6">"</div>
                  <p class="text-xl text-gray-300 leading-relaxed mb-8 max-w-2xl">
                    {{ testimonial.content }}
                  </p>
                  <div class="flex gap-1 mb-6">
                    <span
                      v-for="star in testimonial.rating"
                      :key="star"
                      class="text-yellow-500 text-xl"
                    >
                      ★
                    </span>
                  </div>
                  <div class="flex items-center gap-4">
                    <img
                      :src="testimonial.image"
                      :alt="testimonial.name"
                      class="w-12 h-12 rounded-full object-cover border-2 border-yellow-500"
                    />
                    <div class="text-left">
                      <h4 class="font-semibold text-white">{{ testimonial.name }}</h4>
                      <p class="text-gray-400 text-sm">{{ testimonial.role }}</p>
                    </div>
                  </div>
                </div>
              </div>
            </transition-group>
          </div>

          <!-- Navigation Dots -->
          <div class="absolute -bottom-12 left-1/2 -translate-x-1/2 flex gap-3">
            <button
              v-for="(testimonial, index) in testimonials"
              :key="testimonial.name"
              @click="goToTestimonial(index)"
              class="w-3 h-3 rounded-full transition-all duration-300"
              :class="currentTestimonial === index ? 'bg-yellow-500 scale-125 animate-pulse-fast' : 'bg-gray-600 hover:bg-gray-500'"
            ></button>
          </div>
        </div>
      </div>

      <!-- Call to Action -->
      <div
        class="text-center space-y-6"
        :class="{ 'opacity-0 translate-y-8': !isVisible, 'opacity-100 translate-y-0': isVisible }"
        style="transition: all 1.2s ease-out 0.6s"
      >
        <p class="text-gray-300 text-lg">Ready to join our success stories?</p>
        <button class="px-8 py-4 bg-yellow-500 hover:bg-yellow-400 text-gray-900 font-semibold rounded-full transition-colors duration-200 animate-pop-in">
          Start Your Journey
        </button>
      </div>
    </div>

  </section>

</template>

<style scoped>
/* Existing animations */
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

@keyframes pulse-slow {
  0%, 100% {
    opacity: 0.6;
  }
  50% {
    opacity: 1;
  }
}

/* New slide animations */
.slide-next-enter-active,
.slide-next-leave-active,
.slide-prev-enter-active,
.slide-prev-leave-active {
  transition: all 0.5s ease-in-out;
  position: absolute;
  width: 100%;
}

/* Slide Next */
.slide-next-enter-from {
  transform: translateX(100%);
  opacity: 0;
}

.slide-next-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}

/* Slide Previous */
.slide-prev-enter-from {
  transform: translateX(-100%);
  opacity: 0;
}

.slide-prev-leave-to {
  transform: translateX(100%);
  opacity: 0;
}

/* Common transitions */
.slide-next-enter-active,
.slide-prev-enter-active {
  z-index: 1;
}

/* Utility classes */
.animate-pop-in {
  animation: pop-in 0.8s ease forwards;
}

.animate-pulse-fast {
  animation: pulse-slow 1s ease-in-out infinite;
}

.animate-pulse-slow {
  animation: pulse-slow 2s ease-in-out infinite;
}
</style>