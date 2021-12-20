<template>
  <div class="container">
    <form @submit.prevent="onSubmit">
      <div class="row justify-content-center">
        <div class="col-7">
          <BaseInput
            label="Email"
            type="email"
            v-model="email"
            :error="emailError"
          />
        </div>
        <div class="col-7 mt-3">
          <BaseInput label="Password" type="password" />
        </div>
        <div class="col-7 mt-3">
          <BaseButton type="submit" class="-fill-gradient">Submit</BaseButton>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
  import BaseInput from '../fields/BaseInput.vue';
  import BaseButton from '../fields/BaseButton.vue';
  import { useField } from 'vee-validate';

  export default {
    components: { BaseButton, BaseInput },
    setup() {
      const email = useField('email', function (value) {
        if (!value) return 'This field is required';

        const regex =
          /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        if (!regex.test(String(value).toLowerCase()))
          return 'Please enter a valid email address';

        return true;
      });

      function onSubmit() {
        alert('Submitted!');
      }

      return {
        email: email.value,
        emailError: email.errorMessage,
        onSubmit,
      };
    },
  };
</script>
