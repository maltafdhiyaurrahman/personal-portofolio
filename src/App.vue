<template>
  <div>
    <Navbar />
    <section id="hero" class="dark-section">
      <Hero />
    </section>
    <section id="about" class="light-section">
      <About />
    </section>
    <section id="about" class="light-section">
      <Skills />
    </section>
    <section id="projects" class="dark-section">
      <Projects />
    </section>
    <section id="contact" class="light-section">
      <Contact />
    </section>
  </div>
</template>

<script setup>
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Projects from './components/Projects.vue'
import Contact from './components/Contact.vue'
</script>
