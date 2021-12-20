<template>
  <div class="container">
    <form @submit.prevent="onSubmit">
      <div class="row justify-content-center">
        <div class="col-7">
          <BaseInput
            label="Email"
            type="email"
            :modelValue="emailValue"
            :error="emailError"
            @change="handleChange"
          />
        </div>
        <div class="col-7 mt-3">
          <BaseInput
            label="Password"
            type="password"
            v-model="passwordValue"
            :error="passwordError"
          />
        </div>
        <div class="col-7 mt-3">
          <BaseButton type="submit" class="-fill-gradient">Submit</BaseButton>
        </div>
      </div>
    </form>
  </div>
</template>

<script setup>
  import BaseInput from '../fields/BaseInput.vue';
  import BaseButton from '../fields/BaseButton.vue';
  import { useField, useForm } from 'vee-validate';
  import { object, string, boolean, number } from 'yup';

  // const validations = {
  //   email: (value) => {
  //     if (!value) return 'This field is required';

  //     const regex =
  //       /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
  //     if (!regex.test(String(value).toLowerCase()))
  //       return 'Please enter a valid email address';

  //     return true;
  //   },
  //   password: (value) => {
  //     const requiredMessage = 'This field is required';
  //     if (value === undefined || value === null) return requiredMessage;
  //     if (!String(value).length) return requiredMessage;

  //     return true;
  //   },
  // };

  const validations = object({
    email: string().required().email(),
    password: string().required(),
  });

  const { setFieldValue } = useForm({
    validationSchema: validations,
  });

  const { value: emailValue, errorMessage: emailError } = useField('email');
  const { value: passwordValue, errorMessage: passwordError } =
    useField('password');
  const handleChange = (event) => setFieldValue('email', event.target.value);
</script>
