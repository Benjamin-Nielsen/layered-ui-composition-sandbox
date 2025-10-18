<script setup>
defineProps({
  textMessage: {
    type: String,
    required: false,
  },
})
</script>

<template>
  <div class="text-base-content/60 flex items-center gap-2 px-1 pt-1 text-[0.6875rem]">
    <slot name="start"></slot>
    <span class="status status-error inline-block"></span>
    {{ textMessage }}
    <slot name="end"></slot>
  </div>
</template>

<style scoped></style>
