<template>
  <main>
    <Navbar />
    <Hero />
    <Cocktails />
    <About />
    <Art />
  </main>
</template>

<script setup>
import { gsap } from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
import { SplitText } from "gsap/all";

import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";
import Cocktails from "./components/Cocktails.vue";
import About from "./components/About.vue";
import Art from "./components/Art.vue";

gsap.registerPlugin(ScrollTrigger, SplitText);
</script>
