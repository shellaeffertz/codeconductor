<script setup>
const generateHexColor = () => {
  const colors = ['#FF10F0', '#00FF8F', '#00B8FF', '#FFB800', '#FF0035'];
  return colors[Math.floor(Math.random() * colors.length)];
};
</script>

<template>
  <div class="hidden sm:block fixed inset-0 overflow-hidden bg-[#080610]">
    <!-- Digital Life Forms -->
    <template v-for="i in 15" :key="`lifeform-${i}`">
      <div
        class="absolute"
        :style="{
          top: `${(i * 23) % 90}vh`,
          left: `${(i * 27) % 90}vw`,
        }"
      >
        <!-- Core -->
        <div 
          class="relative w-16 h-16 rounded-full"
          :style="{
            background: `conic-gradient(from ${i * 45}deg, ${generateHexColor()}, transparent)`,
            animation: `spin ${10 + (i % 5)}s linear infinite`,
            filter: 'blur(1px)'
          }"
        >
          <!-- Data Tendrils -->
          <template v-for="j in 6" :key="`tendril-${j}`">
            <div
              class="absolute w-1 origin-bottom"
              :style="{
                height: `${40 + (j * 10)}px`,
                background: `linear-gradient(to top, ${generateHexColor()}, transparent)`,
                transform: `rotate(${j * 60}deg)`,
                animation: `wave ${5 + (j % 3)}s ease-in-out infinite`,
                animationDelay: `${j * 0.5}s`,
                left: '50%',
                top: '-40px'
              }"
            >
              <!-- Data Particles -->
              <div
                class="absolute top-0 left-1/2 w-2 h-2"
                :style="{
                  background: generateHexColor(),
                  animation: `float ${3 + (j % 2)}s ease-in-out infinite`,
                  transform: 'translate(-50%, -50%)',
                  boxShadow: `0 0 10px ${generateHexColor()}`
                }"
              ></div>
            </div>
          </template>
        </div>
      </div>
    </template>

    <!-- Neural Network Connections -->
    <template v-for="i in 20" :key="`connection-${i}`">
        <svg class="absolute inset-0 w-full h-full" style="filter: blur(1px)">
            <path
            :d="`M${(i * 37) % 100},${(i * 17) % 100} Q${50 + Math.sin(i) * 50},${50 + Math.cos(i) * 50} ${(i * 67) % 100},${(i * 89) % 100}`"
            :style="{
                stroke: generateHexColor(),
                strokeWidth: '0.5',
                fill: 'none',
                opacity: 0.3,
                animation: `pulse ${7 + (i % 4)}s ease-in-out infinite`
            }"
            />
        </svg>
    </template>

    <!-- Data Clouds -->
    <template v-for="i in 8" :key="`cloud-${i}`">
      <div
        class="absolute rounded-full mix-blend-screen"
        :style="{
          width: `${200 + (i * 50)}px`,
          height: `${200 + (i * 50)}px`,
          background: `radial-gradient(circle at center, ${generateHexColor()}33 0%, transparent 70%)`,
          filter: 'blur(50px)',
          top: `${(i * 27) % 80}vh`,
          left: `${(i * 31) % 80}vw`,
          animation: `breathe ${15 + (i * 2)}s ease-in-out infinite`,
          transform: `rotate(${i * 45}deg)`
        }"
      ></div>
    </template>

    <!-- Binary Rain -->
    <template v-for="i in 20" :key="`binary-${i}`">
      <div
        class="absolute font-mono text-xs whitespace-nowrap"
        :style="{
          color: generateHexColor(),
          opacity: 0.4,
          top: '-20px',
          left: `${(i * 5)}vw`,
          animation: `fall ${10 + (i % 5)}s linear infinite`,
          animationDelay: `${i * 0.5}s`,
          transform: `rotate(${90 + (i % 10)}deg)`
        }"
      >
        {{ Array.from({length: 10}, () => Math.random() > 0.5 ? '1' : '0').join('') }}
      </div>
    </template>

    <!-- Geometric Shapes -->
    <template v-for="i in 10" :key="`shape-${i}`">
      <div
        class="absolute border-2 w-20 h-20"
        :style="{
          borderColor: generateHexColor(),
          top: `${(i * 33) % 85}vh`,
          left: `${(i * 41) % 85}vw`,
          transform: `rotate(${i * 36}deg)`,
          animation: `morph ${20 + (i % 8)}s ease-in-out infinite`,
          opacity: 0.3
        }"
      ></div>
    </template>
  </div>
</template>

<style scoped>
@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes wave {
  0%, 100% {
    transform: var(--tw-transform) scaleY(0.8);
  }
  50% {
    transform: var(--tw-transform) scaleY(1.2);
  }
}

@keyframes float {
  0%, 100% {
    transform: translate(-50%, -50%) scale(0.8);
  }
  50% {
    transform: translate(-50%, -50%) scale(1.2);
  }
}

@keyframes pulse {
  0%, 100% {
    stroke-dasharray: 0, 1000;
  }
  50% {
    stroke-dasharray: 1000, 0;
  }
}

@keyframes breathe {
  0%, 100% {
    transform: var(--tw-transform) scale(0.8);
    opacity: 0.3;
  }
  50% {
    transform: var(--tw-transform) scale(1.2);
    opacity: 0.6;
  }
}

@keyframes fall {
  0% {
    transform: translateY(-100vh) var(--tw-transform);
    opacity: 0;
  }
  10% {
    opacity: 0.4;
  }
  90% {
    opacity: 0.4;
  }
  100% {
    transform: translateY(200vh) var(--tw-transform);
    opacity: 0;
  }
}

@keyframes morph {
  0%, 100% {
    clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
    transform: var(--tw-transform) rotate(0deg);
  }
  25% {
    clip-path: polygon(25% 0%, 100% 25%, 75% 100%, 0% 75%);
    transform: var(--tw-transform) rotate(90deg);
  }
  50% {
    clip-path: polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%);
    transform: var(--tw-transform) rotate(180deg);
  }
  75% {
    clip-path: polygon(50% 0%, 100% 100%, 50% 100%, 0% 0%);
    transform: var(--tw-transform) rotate(270deg);
  }
}
</style>