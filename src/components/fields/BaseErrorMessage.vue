<template>
  <p aria-live="assertive" class="text-danger" :id="id">
    <slot />
  </p>
</template>

<script setup>
  defineProps({
    id: {
      type: [String, Number],
      required: true,
    },
  });
</script>
