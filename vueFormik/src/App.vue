<script setup>
import Formik from './components/lib/Formik.vue';
import { ref, reactive } from 'vue';

const validate = (values) => {
  const errors = {};
  if (!values.email) {
    errors.email = 'Required';
  } else if (
    !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
  ) {
    errors.email = 'Invalid email address';
  }
  return errors;
}

const initialValues = reactive({
  email: '',
  password: ''
});

const onSubmit = (values, { setSubmitting }) => {
  setTimeout(() => {
    alert(JSON.stringify(values, null, 2));
    setSubmitting(false);
  }, 400);
}
</script>

<template>
  <header>
  </header>

  <main>
    <Formik :initialValues="initialValues" :validate="validate" :onSubmit="onSubmit"
     v-slot="{ values, errors, handleSubmit, isSubmitting }">
      <form @submit.prevent="handleSubmit">
        <input type="text" />
        <button type="submit">Submit</button>

      </form>
    </Formik>

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
