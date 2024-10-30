<script setup> 

</script>

<template>

    <div 
        class="max-w-3xl mx-auto text-center space-y-6 animate-on-scroll"
        style="transition: all 0.8s ease-out 1.4s"
      >
        <h3 class="text-2xl font-bold text-yellow-500">
            <slot name="title" />
        </h3>
        <p class="text-gray-300 leading-relaxed">
          <slot name="description" />
        </p>
        <button class="px-8 py-4 bg-yellow-500 hover:bg-yellow-400 text-gray-900 font-semibold rounded-full transition-colors duration-200 animate-pop-in mt-4">
          <slot name="btn-label" />
        </button>
    </div>

</template>

<style scoped>

.animate-on-scroll {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s ease;
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

</style>