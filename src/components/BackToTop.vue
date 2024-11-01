<script setup>

import { onMounted } from 'vue';

window.addEventListener('scroll', function() {
    if(this.scrollY >= 750) {
        if(toTopBtn.classList.contains('-right-14')) {
            toTopBtn.classList.remove('-right-14');
            toTopBtn.classList.add('right-5');
        }
    } else {
        if(toTopBtn.classList.contains('right-5')) {
            toTopBtn.classList.remove('right-5');
            toTopBtn.classList.add('-right-14');
        }
    }
});

onMounted(() => {
    toTopBtn.addEventListener('click', () => {
        window.scrollTo({
            top: 0
        });
    });
});

</script>

<template>
    
    <button id="toTopBtn" class="block w-14 h-14 rounded-full border border-yellow-500 bg-gradient-to-r from-yellow-500 via-amber-400 to-yellow-300 hover:bg-yellow-400 fixed z-50 bottom-10 -right-14 duration-200 animate-bounce" type="button">
        <i class="fa-solid fa-arrow-up font-black text-gray-900 text-xl"></i>
    </button>

</template>