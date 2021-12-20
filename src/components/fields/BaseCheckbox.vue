<template>
  <input
    v-bind="{ ...$attrs, onChange: updateValue }"
    :checked="modelValue"
    :id="uuid"
    type="checkbox"
    class="form-check-input"
  />
  <label :for="uuid" v-if="label" class="form-check-label">
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
      type: Boolean,
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
