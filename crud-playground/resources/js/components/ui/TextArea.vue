<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';

const props = defineProps<{
  modelValue: string;
  id?: string;
  rows?: number;
  required?: boolean;
}>();

const emit = defineEmits(['update:modelValue']);

function onInput(event: Event) {
  const target = event.target as HTMLTextAreaElement | null;
  if (target) {
    emit('update:modelValue', target.value);
  }
}
</script>

<template>
  <textarea
    :id="id"
    :rows="rows ?? 3"
    :required="required"
    class="w-full border rounded px-3 py-2"
    :value="modelValue"
    @input="onInput"
  />
</template>
