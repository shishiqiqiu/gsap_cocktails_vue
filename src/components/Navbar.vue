<template>
  <nav>
    <div>
      <a href="#home" class="flex items-center gap-2">
        <AppImage src="/images/logo.png" alt="logo" />
        <p>Velvet Pour</p>
      </a>
      <ul>
        <li v-for="link in navLinks" :key="link.id">
          <a :href="'#' + link.id">{{ link.title }}</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
import { onMounted, onUnmounted } from "vue";
import { gsap } from "gsap";

import { navLinks } from "../../constants";
import AppImage from "./AppImage.vue";

let ctx, navTween;
onMounted(() => {
  ctx = gsap.context(() => {
    navTween = gsap.timeline({
      scrollTrigger: {
        trigger: "nav",
        start: "bottom top",
      },
    });

    navTween.fromTo(
      "nav",
      { backgroundColor: "transparent" },
      {
        backgroundColor: "#00000050",
        backdropFilter: "blur(10px)",
        duration: 1,
        ease: "power1.inOut",
      }
    );
  });
});
onUnmounted(() => {
  ctx?.revert();
});
</script>
