<template>
  <label v-if="label" :for="uuid">{{ label }}</label>
  <input
    class="form-control"
    v-bind="{
      ...$attrs,
      onInput: updateValue,
    }"
    :id="uuid"
    :value="modelValue"
    :placeholder="label"
    :aria-describedby="error ? `${uuid}-error` : null"
    :aria-invalid="error ? true : false"
    :class="{ error }"
  />
  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">{{
    error
  }}</BaseErrorMessage>
</template>

<script setup>
  import SetupFormComponent from '../../features/SetupFormComponent';
  import UniqueID from '../../features/UniqueID';
  import BaseErrorMessage from './BaseErrorMessage.vue';

  const props = defineProps({
    label: {
      type: String,
      default: '',
    },
    error: {
      type: String,
      default: '',
    },
    modelValue: {
      type: [String, Number],
      default: '',
    },
  });
  const emit = defineEmits(['update:modelValue']);
  const { updateValue } = SetupFormComponent(props, emit);
  const uuid = UniqueID().getID();
</script>
