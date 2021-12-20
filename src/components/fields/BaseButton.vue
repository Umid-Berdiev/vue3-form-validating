<template>
  <button :class="classes">
    <slot />
  </button>
</template>

<script setup>
  defineProps({
    classes: {
      type: String,
      default: 'btn btn-success',
    },
  });
</script>
