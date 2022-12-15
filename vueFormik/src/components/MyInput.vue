<script setup>
const props = defineProps({
    values: {
        type: Object,
        required: true
    },
});
const updateFirstname = (event) => {
    props.values.firstname = event.target.value;
}

const updateLastname = (event) => {
    props.values.lastname = event.target.value;
}
</script>

<template>
  <input
    @input="updateFirstname"
    :value="values.firstname"
  />
  <input
    @input="updateLastname"
    :value="values.lastname"
  />
</template>
