<template>
  <main>
    <Navbar />
  </main>
</template>

<script setup>
import { gsap } from "gsap";
import { ScrollTrigger, SplitText } from "gsap/all";

import Navbar from "./components/Navbar.vue";

gsap.registerPlugin(ScrollTrigger, SplitText);
</script>
