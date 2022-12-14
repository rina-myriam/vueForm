<script setup>
defineProps({
 
  value: {
    type: Object,
  },
});
const options = Array.from({ length: 9 }, (_, i) => ({
  id: i,
  href: `https://picsum.photos/200?random=${i}`,
}));
</script>

<template>
  <div class="grid">
    <img
      :src="option.href"
      alt="Captcha"
      v-for="option in options"
      :key="option.id"
      :class="{ selected: option.id === value?.id }"
      @click="$emit('update:value', option)"
    />
  </div>
</template>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}
img {
  width: 100%;
  cursor: pointer;
}
img.selected {
  border: 5px solid magenta;
}
</style>
