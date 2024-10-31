<script setup>

import { ref, onMounted, onBeforeUnmount} from 'vue';

let codeSymbols = ref([]);

let symbolPool = ref([
    '{ }', '[ ]', '( )', '</ >', '=>', '&&', '||', 
    '++', '--', '**', '//', '/*', '*/', 
    '===', '!==', '??', '?.', '|>', 
    'async', 'await', 'import', 'export'
]);

const createCodeSymbol = () => {

      return {
        id: Date.now() + Math.random(),
        symbol: symbolPool.value[Math.floor(Math.random() * symbolPool.value.length)],
        left: Math.random() * 100,
        animationDuration: 10 + Math.random() * 15,
        delay: Math.random() * 5,
        size: 10 + Math.random() * 30,
        color: `hsl(${Math.random() * 360}, 50%, 50%)`
      };
}

const generateInitialSymbols = () => {
    codeSymbols.value = Array(50).fill().map(() => createCodeSymbol());
};

const handleScroll = () => {

      if (Math.random() < 0.3) {
        codeSymbols.value.push(this.createCodeSymbol());
        
        if (codeSymbols.value.length > 100) {
          codeSymbols.value.shift();
        }
      }
};

onMounted(() => {

  generateInitialSymbols();

  window.addEventListener('scroll', handleScroll);

});

onBeforeUnmount(() => {

  window.removeEventListener('scroll', handleScroll);

});

</script>

<template>
  <div 
    ref="backgroundContainer"
    class="fixed inset-0 z-[-1] bg-gradient-to-br from-gray-900 via-gray-800 to-gray-900 overflow-hidden"
  >
    <div 
      v-for="symbol in codeSymbols" 
      :key="symbol.id"
      class="absolute text-green-500 font-mono font-bold opacity-30 select-none"
      :style="{
        left: `${symbol.left}%`,
        fontSize: `${symbol.size}px`,
        animation: `fall-symbol ${symbol.animationDuration}s linear infinite`,
        animationDelay: `-${symbol.delay}s`,
        color: symbol.color
      }"
    >
      {{ symbol.symbol }}
    </div>

    <!-- Grid Overlay -->
    <div 
      class="absolute inset-0 pointer-events-none opacity-10"
      :style="{
        backgroundImage: `
          linear-gradient(0deg, transparent 24%, rgba(255,255,255,0.05) 25%, rgba(255,255,255,0.05) 26%, transparent 27%),
          linear-gradient(90deg, transparent 24%, rgba(255,255,255,0.05) 25%, rgba(255,255,255,0.05) 26%, transparent 27%)
        `,
        backgroundSize: '50px 50px'
      }"
    />
  </div>
</template>

<style>
@keyframes fall-symbol {
  0% {
    transform: translateY(-100vh) rotate(0deg);
    opacity: 0.3;
  }
  100% {
    transform: translateY(100vh) rotate(360deg);
    opacity: 0.1;
  }
}
</style>