<script setup>
import { ref, reactive, inject } from 'vue';
const isSubmitting = ref(false);
const errors = reactive([]);

const props = defineProps({
    initialValues: {
        type: Object,
        required: true,
    },
    validate: {
        type: Function,
        required: true
    },
    onSubmit: {
        type: Function,
        required: true
    },
});
const values = reactive(props.initialValues);

const setSubmitting = (value) => {
    isSubmitting.value = value;
}

const handleSubmit = () => {
    errors.push(props.validate(values));
    if (errors.length === 0) {
        props.onSubmit(values, setSubmitting);
    }
    console.log(values);
}
//const value = inject("value:value");

</script>

<template>
    <slot :values="values" :errors="errors" :handleSubmit="handleSubmit"  :isSubmitting="isSubmitting">
    </slot>
</template>
