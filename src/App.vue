<template>
  <main>
    <Navbar />
    <Hero />
    <Cocktails />
  </main>
</template>

<script setup>
import { gsap } from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
import { SplitText } from "gsap/all";

import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";
import Cocktails from "./components/Cocktails.vue";

gsap.registerPlugin(ScrollTrigger, SplitText);
</script>
