<script setup>

</script>

<template>

    <div class="text-center space-y-4 animate-on-scroll" style="transition: all 0.8s ease-out 0.2s">
        <h3 class="text-yellow-500 text-xl font-medium tracking-wide animate-pop-in">
            <slot name="subtitle" />
        </h3>
        <h2 class="font-black text-5xl md:text-6xl bg-gradient-to-r from-white to-gray-300 bg-clip-text animate-gradient-pop">
            <slot name="title" />
        </h2>
        <p class="max-w-2xl mx-auto text-gray-300 text-lg">
          <slot name="description" />
        </p>
        <div class="h-2 w-24 bg-yellow-500 rounded-full mx-auto animate-pulse-fast"></div>
    </div>


</template>

<style scoped>

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

.animate-on-scroll {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s ease;
}

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
}

.animate-pulse-fast {
  animation: pulse-slow 1s ease-in-out infinite;
}

@keyframes pulse-slow {
  0%, 100% {
    opacity: 0.6;
  }
  50% {
    opacity: 1;
  }
}

</style>