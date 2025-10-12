<script setup>
defineProps({
  textMessage: {
    type: String,
    required: false,
  },
})
</script>

<template>
  <div class="text-red pl-2 text-sm pb-3 pt-1">
    <slot name="start"></slot>
    {{textMessage}}
    <slot name="end"></slot>
  </div>
</template>

<style scoped>
.text-red {
  color: red;
}
</style>
