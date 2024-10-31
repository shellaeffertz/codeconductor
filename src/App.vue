<script setup>

import Navbar from './components/Navbar.vue';
import Home from './components/Home.vue';
import AboutUs from './components/AboutUs.vue';
import Contact from './components/Contact.vue';
import Projects from './components/Projects.vue';
import BackToTop from './components/BackToTop.vue';
import OurSkills from './components/OurSkills.vue';
import WhatCanWeDo from './components/WhatCanWeDo.vue';
import Testimonials from './components/Testimonials.vue';
import FooterSection from './components/FooterSection.vue';
import ScrollProgress from './components/ScrollProgress.vue';
import BackgroundView from './components/BackgroundView.vue';

</script>

<template>

  <ScrollProgress />

  <Navbar />

  <BackgroundView />

  <Home id="home" class="mt-16 sm:mt-0" />

  <AboutUs id="about-us" />
  
  <WhatCanWeDo id="services" />

  <Testimonials />

  <OurSkills />

  <Projects id="projects" />

  <Contact id="contact" />

  <FooterSection />

  <BackToTop />

</template>

<style>

html {
  scroll-behavior: smooth;
}

::-webkit-scrollbar {
  width: 6px;
}

::-webkit-scrollbar-track {
  background: linear-gradient(to bottom right, #111827, #1f2937, #111827);
  border-radius: 8px;
}

::-webkit-scrollbar-thumb {
  background-color: #eab308;
  border-radius: 8px;
  border: 2px solid #1f2937;
}

::-webkit-scrollbar-thumb:hover {
  background-color: #facc15;
}

</style>
