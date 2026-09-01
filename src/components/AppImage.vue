<template>
  <picture class="contents">
    <source :srcset="webpSrc" type="image/webp" />
    <img :src="src" v-bind="$attrs" />
  </picture>
</template>

<script setup>
import { computed } from "vue";

defineOptions({
  inheritAttrs: false,
});

const props = defineProps({
  src: {
    type: String,
    required: true,
  },
  webp: {
    type: String,
    default: "",
  },
});

const webpSrc = computed(() => {
  if (props.webp) {
    return props.webp;
  }

  return props.src.replace(/\.(png|jpe?g|gif)$/i, ".webp");
});
</script>
