
<template>
    <slot :name="name" >
        <component :is="dynamicComponent" 
        v-model="value"
    :value="value"></component>
    {{name}}
    </slot>
</template>

<script setup>
import { ref } from 'vue';
import { ref, provide } from 'vue';

const field = ref(null)

const value = ref('');

defineProps({
    name: {
        type: String,
        default: ''
    },
    dynamicComponent: {
        type: String,
        default: ''
    },
});
provide('field', field);
</script>