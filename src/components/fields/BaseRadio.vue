<template>
  <input
    type="radio"
    v-bind="{ ...$attrs, onChange: updateValue }"
    :checked="modelValue === value"
    :id="uuid"
    class="form-check-input"
  />
  <label v-if="label" :for="uuid" class="form-check-label">
    {{ label }}
  </label>
  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">
    {{ error }}
  </BaseErrorMessage>
</template>

<script setup>
  import UniqueID from '../../features/UniqueID';
  import SetupFormComponent from '../../features/SetupFormComponent';
  import BaseErrorMessage from './BaseErrorMessage.vue';

  const props = defineProps({
    label: {
      type: String,
      default: '',
    },
    modelValue: {
      type: [String, Number],
    },
    value: {
      type: [String, Number],
    },
    error: {
      type: String,
      default: '',
    },
  });

  const emit = defineEmits(['update:modelValue']);

  const uuid = UniqueID().getID();
  const { updateValue } = SetupFormComponent(props, emit);
</script>
