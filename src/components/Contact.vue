<template>
  <footer id="contact">
    <AppImage
      src="/images/footer-right-leaf.png"
      alt="leaf-right"
      id="f-right-leaf"
    />
    <AppImage src="/images/footer-left-leaf.png" alt="leaf-left" id="f-left-leaf" />
    <div class="content">
      <h2>Where to Find Us</h2>
      <div>
        <h3>Visit Our Bar</h3>
        <p>123, Raq Blvd. 456, Los Angeles</p>
      </div>
      <div>
        <h3>Contact Us</h3>
        <p>(12) 345-6789</p>
        <p>zyb@exmaple.com</p>
      </div>

      <div>
        <h3>Open Every Day</h3>
        <p v-for="time in openingHours" :key="time.day">
          {{ time.day }} : {{ time.time }}
        </p>
      </div>

      <div>
        <h3>Socials</h3>
        <div class="flex-center gap-5">
          <a
            v-for="social in socials"
            :key="social.name"
            :href="social.url"
            target="_blank"
            rel="noopener noreferrer"
            :aria-label="social.name"
            ><AppImage :src="social.icon"
          /></a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { onMounted, onUnmounted } from "vue";
import { openingHours, socials } from "../../constants";
import AppImage from "./AppImage.vue";
import { SplitText } from "gsap/all";
import gsap from "gsap";

let ctx, titleSplit, timeline;
onMounted(() => {
  ctx = gsap.context(() => {
    titleSplit = SplitText.create("#contact h2", { type: "words" });

    timeline = gsap.timeline({
      scrollTrigger: {
        trigger: "#contact",
        start: "top center",
      },
      ease: "power1.inOut",
    });

    timeline
      .from(titleSplit.words, {
        opacity: 0,
        yPercent: 100,
        stagger: 0.02,
      })
      .from("#contact h3, #contact p", {
        opacity: 0,
        yPercent: 100,
        stagger: 0.02,
      })
      .to("#f-right-leaf", {
        y: "-50",
        duration: 1,
        ease: "power1.inOut",
      })
      .to(
        "#f-left-leaf",
        {
          y: "-50",
          duration: 1,
          ease: "power1.inOut",
        },
        "<"
      );
  });
});
onUnmounted(() => {
  titleSplit?.revert();
  ctx?.revert();
});
</script>
