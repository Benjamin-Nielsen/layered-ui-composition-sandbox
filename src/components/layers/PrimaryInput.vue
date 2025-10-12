<script setup>
import { ref, computed } from "vue";
import StrippedButton from "./StrippedButton.vue";

const props = defineProps({
  placeholder: {
    type: String,
    required: true,
  },
  type: {
    type: String,
    required: false,
    default: 'text',
  },
});
const message = defineModel();
const showPassword = ref(false);
const computedType = computed(() => {
  if(!props.type == 'password') {
    return props.type;
  }
  if(showPassword.value) {
    return 'text';
  }
  return props.type;
});

const buttonPressed = () => {
  showPassword.value = !showPassword.value;


};
</script>

<template>
  <div class="flex text-white bg-brand border border-brand-500 rounded not-data-disabled:hover:bg-brand-600 data-disabled:bg-brand-300 data-disabled:text-gray">
    <input
      v-model="message"
      :placeholder="placeholder"
      :type="computedType"
      class="p-2 flex-grow"
    />
    <!-- The showPassword button slot. -->
    <button
      @click="buttonPressed"
      v-if="$slots.button || type == 'password'"
      class="flex justify-items-stretch align-items-center"
    >
      <!-- Default label for the showPassword button -->
      <slot name="button" :showPassword="showPassword">
        <StrippedButton v-if="showPassword">Show</StrippedButton>
        <StrippedButton v-else>Hide</StrippedButton>
      </slot>
    </button>
  </div>
</template>

<style scoped></style>
