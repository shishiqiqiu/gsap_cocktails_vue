<template>
  <main>
    <Navbar />
    <Hero />
  </main>
</template>

<script setup>
import { gsap } from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
import { SplitText } from "gsap/all";

import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";

gsap.registerPlugin(ScrollTrigger, SplitText);
</script>
