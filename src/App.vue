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

  <Home />

  <AboutUs />
  
  <WhatCanWeDo />

  <Testimonials />

  <OurSkills />

  <Projects />

  <Contact />

  <FooterSection />

  <BackToTop />

</template>

<style>

html {
  scroll-behavior: smooth;
}

</style>
