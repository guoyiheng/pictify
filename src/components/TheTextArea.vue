<script setup lang="ts">
const { modelValue } = defineModel<{
  modelValue: string
}>()
</script>

<template>
  <textarea
    v-model="modelValue"
    rows="4"
    type="text"
    v-bind="$attrs"
    p="x-4 y-2"
    bg="transparent"
    border="~ rounded gray-200 dark:gray-700"
    outline="none active:none"
  />
</template>
