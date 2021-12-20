<template>
  <label v-if="label" :for="uuid">
    {{ label }}
  </label>
  <select
    class="form-select"
    v-bind="{
      ...$attrs,
      onChange: updateValue,
    }"
    :value="modelValue"
    :id="uuid"
    :aria-describedby="error ? `${uuid}-error` : null"
    :aria-invalid="error ? true : false"
    :class="{ error }"
  >
    <option
      v-for="option in options"
      :value="option"
      :key="option"
      :selected="option === modelValue"
    >
      {{ option }}
    </option>
  </select>
  <BaseErrorMessage v-if="error" :id="`${uuid}-error`">
    {{ error }}
  </BaseErrorMessage>
</template>

<script setup>
  import SetupFormComponent from '../../features/SetupFormComponent';
  import UniqueID from '../../features/UniqueID';
  import BaseErrorMessage from '../fields/BaseErrorMessage.vue';

  const props = defineProps({
    options: {
      type: Array,
      required: true,
    },
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
    },
  });
  const emit = defineEmits(['update:modelValue']);
  const { updateValue } = SetupFormComponent(props, emit);
  const uuid = UniqueID().getID();
</script>
