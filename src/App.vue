<template>
  <main>
    <Navbar />
    <Hero />
    <div class="h-dvh bg-black"></div>
  </main>
</template>

<script setup>
import { gsap } from "gsap";
import { ScrollTrigger, SplitText } from "gsap/all";

import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";

gsap.registerPlugin(ScrollTrigger, SplitText);
</script>
