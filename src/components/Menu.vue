<template>
  <section id="menu" aria-labelledby="menu-heading">
    <img src="/images/slider-left-leaf.png" alt="left-leaf" id="m-left-leaf" />
    <img
      src="/images/slider-right-leaf.png"
      alt="right-leaf"
      id="m-right-leaf"
    />

    <h2 id="menu-heading" class="sr-only">Cocktials Menu</h2>

    <nav class="cocktail-tabs" aria-label="Cocktail Navigation">
      <button
        v-for="(cocktail, index) in allCocktails"
        :key="cocktail.id"
        :class="[
          currentIndex === index
            ? 'text-white border-white'
            : 'text-white/50 border-white/50',
        ]"
        @click="goToSlide(index)"
      >
        {{ cocktail.name }}
      </button>
    </nav>

    <div class="content">
      <div class="arrows">
        <button class="text-left" @click="goToSlide(currentIndex - 1)">
          <span>{{ prevCocktail.name }}</span>
          <img
            src="/images/right-arrow.png"
            alt="right-arrow"
            aria-hidden="true"
          />
        </button>
        <button class="text-left" @click="goToSlide(currentIndex + 1)">
          <span>{{ nextCocktail.name }}</span>
          <img
            src="/images/left-arrow.png"
            alt="left-arrow"
            aria-hidden="true"
          />
        </button>
      </div>

      <div class="cocktail">
        <img :src="currentCocktail.image" class="object-contain" />
      </div>

      <div class="recipe">
        <div class="info">
          <p>Recipe for:</p>
          <p id="title">{{ currentCocktail.name }}</p>
        </div>

        <div class="details">
          <h2>{{ currentCocktail.title }}</h2>
          <p>{{ currentCocktail.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed, onMounted, ref, watch } from "vue";
import { allCocktails } from "../../constants";
import gsap from "gsap";

const currentIndex = ref(0);

const totalCocktails = allCocktails.length;

const getCocktailAt = (offset) => {
  return allCocktails[
    (currentIndex.value + offset + totalCocktails) % totalCocktails
  ];
};

const currentCocktail = computed(() => getCocktailAt(0));
const prevCocktail = computed(() => getCocktailAt(-1));
const nextCocktail = computed(() => getCocktailAt(1));

const goToSlide = (index) => {
  currentIndex.value = (index + totalCocktails) % totalCocktails;
};

const runAnimation = () => {
  gsap.fromTo("#title", { opacity: 0 }, { opacity: 1, duration: 1 });

  gsap.fromTo(
    ".cocktail img",
    { opacity: 0, xPercent: -100 },
    { opacity: 1, xPercent: 0, duration: 1, ease: "power1.inOut" }
  );

  gsap.fromTo(
    ".details h2",
    { yPercent: 100, opacity: 0 },
    { yPercent: 0, opacity: 1, ease: "power1.inOut" }
  );

  gsap.fromTo(
    ".details p",
    { yPercent: 100, opacity: 0 },
    { yPercent: 0, opacity: 1, ease: "power1.inOut" }
  );
};

onMounted(() => {
  runAnimation();
});

watch(currentIndex, () => {
  runAnimation();
});
</script>
