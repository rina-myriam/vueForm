<template>
    <Field ref="field">
        <div> Input </div>
    </Field>
</template>

<script setup>
import Field from './Field.vue';
import { ref, provide } from 'vue';

const field = ref(null)
provide('field', field);
</script>
