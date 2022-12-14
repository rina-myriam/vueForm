<script setup>
import Field from './components/lib/Field.vue';
import { ref } from 'vue';
const name =  ref("test");
const input = ref("Input");
const modelValue = ref("test");
</script>

<template>
  <header>
  </header>

  <main>
    <Field :name="name" :dynamicComponent="input" v-model:value="modelValue" >
      {{ value }}
    </Field>

  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
