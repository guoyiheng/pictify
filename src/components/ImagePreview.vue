<script setup lang="ts">
defineProps<{
  source: string
}>()
defineOptions({
  name: 'Preview',
})
const { show } = defineModel<{
  show: boolean
}>()
</script>

<template>
  <Transition name="fade">
    <div v-show="show" fixed z-10 flex bg-white dark:bg-hex-121212 inset-0 items-center justify-center>
      <img :src="source" h-full w-auto @click="show = false">
    </div>
  </Transition>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
