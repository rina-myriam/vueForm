<script setup>
import { ref, provide, reactive } from 'vue';
const isSubmitting = ref(false);
const errors = ref({});

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
    errors.value = props.validate(values);
    if (errors.value.length === 0) {
        props.onSubmit(values, setSubmitting);
    }
}
provide("globalValuesForm:values", values);

</script>

<template>
    <slot :values="values" :errors="errors" :handleSubmit="handleSubmit"  :isSubmitting="isSubmitting">
    </slot>
</template>
