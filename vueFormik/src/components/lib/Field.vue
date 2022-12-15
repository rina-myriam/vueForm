<script setup>
import { provide, inject, reactive, onUpdated } from 'vue';


const props = defineProps({
    name: {
        type: String,
        required: true
    },
    as: {
        type: [String, Object],
        default: 'input'
    },
    modelValue: {
        type: [String, Object],
        default: ''
    }
});


const emit = defineEmits(['update:modelValue'])

const updateValue = (event) => {
    emit('update:modelValue', event.target.value)
}

const values = inject("globalValuesForm:values");

</script>


<template>
    <slot>
        <div>
            {{ name }} :
            <input v-if="as == 'input' ? true : false" :value="modelValue" @input="updateValue" />
            <textarea v-else-if="as == 'textarea' ? true : false" :value="modelValue" @input="updateValue"></textarea>
            <select v-else-if="as == 'select' ? true : false" :value="modelValue" @input="updateValue">
                <slot name="options"></slot>
            </select>
            <component v-else :is="as" v-bind="{ values }" />
        </div>
    </slot>
</template>
