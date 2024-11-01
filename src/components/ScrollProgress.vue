<script setup>

import { ref, onMounted, onUnmounted } from 'vue';

const scrollProgress = ref(null);
const height = ref(0);

const calculateHeight = () => {
  height.value = document.documentElement.scrollHeight - window.innerHeight;
};

const updateProgress = () => {
  if (!scrollProgress.value) return;
  
  const scrollTop = window.pageYOffset || document.documentElement.scrollTop;
  const scrollPercentage = Math.min((scrollTop / height.value) * 100, 100);
  scrollProgress.value.style.width = `${scrollPercentage}%`;
};

onMounted(() => {
  calculateHeight();
  updateProgress();
  
  window.addEventListener('scroll', updateProgress);
  window.addEventListener('resize', calculateHeight);
  
  const resizeObserver = new ResizeObserver(calculateHeight);
  resizeObserver.observe(document.body);
});

onUnmounted(() => {
  window.removeEventListener('scroll', updateProgress);
  window.removeEventListener('resize', calculateHeight);
});

</script>

<template>

  <span ref="scrollProgress" class="block fixed top-0 left-0 bg-gradient-to-r from-yellow-500 via-amber-400 to-yellow-300 h-1 z-[99999]" style="width: 0%"></span>

</template>

<style scoped>

span {
  transition: width 0.1s ease-out;
}

</style>