<script setup>
import Formik from './components/lib/Formik.vue';
import Field from './components/lib/Field.vue';
import { ref, reactive } from 'vue';
import Captcha from './components/lib/Captcha.vue';
import MyInput from './components/MyInput.vue';
const validate = (values) => {
  const errors = {};
  if (!values.email) {
    errors.email = 'Required';
  } else if (
    !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
  ) {
    errors.email = 'Invalid email address';
  }
  if (!values.password) {
    errors.password = 'Required';
  } else if (values.password.length < 8) {
    errors.password = 'Must be 8 characters or more';
  }
  if (!values.select) {
    errors.select = 'Required';
  }
  if (!values.myInput.lastname || !values.myInput.firstname) {
    errors.myInput = 'Required';
  }
  if (!values.captcha.id) {
    errors.captcha = 'Required';
  }
  return errors;
}

const initialValues = reactive({
  email: '',
  password: '',
  select: '',
  myInput: {
    firstname: '',
    lastname: '',
  },
  captcha: {
    id: '',
    url: '',
  },
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
        <Field name="email" v-model="values.email" />
        <div :style="{ backgroundColor: errors.email ? 'red' : ''  }">{{ errors.email }}</div>
        <Field name="password" v-model="values.password" as="textarea" />
        <div :style="{ backgroundColor: errors.password ? 'red' : ''  }">{{ errors.password }}</div>
        <Field name="select" v-model="values.select" as="select">
          <template v-slot:options>
            <option value="1">One</option>
            <option value="2">Two</option>
            <option value="3">Three</option>
          </template>
        </Field>
        <div :style="{ backgroundColor: errors.select ? 'red' : '' }">{{ errors.select }}</div>
        <Field name="myInput" :as="MyInput"/>
        <div :style="{ backgroundColor: errors.myInput ? 'red' : '' }">{{ errors.myInput }}</div>
        <Field name="captcha" :as="Captcha"/>
        <div :style="{ backgroundColor: errors.captcha ? 'red' : ''  }">{{ errors.captcha }}</div>
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
