<script setup>

import { ref, onMounted } from 'vue';
import EndSection from './EndSection.vue';
import SectionHeader from './SectionHeader.vue';

const copiedContact = ref(null);

const contacts = [
  {
    label: 'Email',
    value: 'info@mycompany.com',
    copyOnClick: true,
    icon: 'fa-solid fa-envelope',
  },
  {
    label: 'Discord',
    value: 'mycompany#1234',
    copyOnClick: true,
    icon: 'fa-brands fa-discord',
  },
  {
    label: 'WhatsApp',
    value: '+1 (555) 123-4567',
    copyOnClick: true,
    icon: 'fa-brands fa-whatsapp',
  },
  {
    label: 'Telegram',
    value: 't.me/mycompany',
    copyOnClick: false,
    icon: 'fa-brands fa-telegram',
  },
];

const handleContactCopy = (value) => {
  navigator.clipboard.writeText(value);
  copiedContact.value = value;
  setTimeout(() => (copiedContact.value = null), 2000);
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
});
</script>

<template>
  <section class="relative max-w-7xl mx-auto px-6 min-h-screen text-white overflow-hidden py-24">
    <div class="relative z-10 space-y-16">

      <SectionHeader>

        <template #subtitle>
          Get in Touch
        </template>

        <template #title>
          Contact Us
        </template>

        <template #description>
          We're here to help! Reach out to us using any of the contact methods below.
        </template>

      </SectionHeader>

      <!-- Contact Cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
        <div
          v-for="(contact, index) in contacts"
          :key="contact.label"
          class="group relative bg-gray-800/30 backdrop-blur-sm rounded-2xl p-6 border border-gray-700/50 hover:border-yellow-500/50 transition-all duration-300 animate-on-scroll animate-slide-in"
          :style="`transition-delay: ${0.4 + index * 0.2}s`"
        >
          <div class="space-y-4">
            <div class="flex items-center justify-center">
              <i :class="[contact.icon, 'fa-2x', 'text-yellow-500', 'animate-bounce']"></i>
            </div>
            <h3 class="text-2xl font-bold text-white group-hover:text-yellow-500 transition-colors duration-300">
              {{ contact.label }}
            </h3>
            <div class="flex items-center justify-between">
              <p class="text-gray-300 text-lg font-medium">{{ contact.value }}</p>
              <button
                v-if="contact.copyOnClick"
                class="p-2 bg-gray-700 rounded-full hover:bg-yellow-500 hover:text-gray-900 transition-colors duration-200 animate-pop-in"
                @click="handleContactCopy(contact.value)"
              >
                <i
                  :class="[
                    copiedContact === contact.value ? 'fa-check-circle' : 'fa-copy',
                    'fa-solid',
                    'w-5',
                    'h-5'
                  ]"
                ></i>
              </button>
              <a
                v-else
                :href="`https://${contact.value}`"
                target="_blank"
                rel="noopener noreferrer"
                class="p-2 bg-gray-700 rounded-full hover:bg-yellow-500 hover:text-gray-900 transition-colors duration-200 animate-pop-in"
              >
                <i class="fa-solid fa-arrow-up-right-from-square w-5 h-5"></i>
              </a>
            </div>
          </div>

          <!-- Hover Effect -->
          <div
            class="absolute inset-0 bg-gradient-to-r from-yellow-500/0 via-yellow-500/5 to-yellow-500/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-2xl animate-scale-up"
          ></div>
        </div>
      </div>

      <EndSection>

        <template #title>
          We’d Love to Hear From You
        </template>

        <template #description>
          Whether you have a question about our services, want to discuss your project, or just want to say hello, feel free to reach out. Our team is here to assist you!
        </template>

        <template #btn-label>
          Contact Us Today
        </template>

      </EndSection>

    </div>
  </section>
</template>

<style scoped>
@keyframes gradient-pop {
  0% {
    background-size: 100%;
    opacity: 0;
  }
  100% {
    background-size: 100%;
    opacity: 1;
  }
}

.animate-gradient-pop {
  animation: gradient-pop 1s ease forwards;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
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

@keyframes slide-in {
  from {
    transform: translateY(50px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.animate-slide-in {
  animation: slide-in 0.8s ease forwards;
}

@keyframes scale-up {
  from {
    transform: scale(0.8);
  }
  to {
    transform: scale(1);
  }
}

.animate-scale-up {
  animation: scale-up 0.4s ease-out forwards;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.animate-bounce {
  animation: bounce 1s ease-in-out infinite;
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