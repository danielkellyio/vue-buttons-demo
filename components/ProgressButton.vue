<script setup lang="ts">
import { defineProps } from 'vue'

const done = refAutoReset(false, 3000)

const props = defineProps<{
  label?: string
  progress?: number
  completeMsg?: string
}>()

watch(() => props.progress, (progress) => {
  if (Number(progress) >= 100) {
    done.value = true
  }
})
</script>

<template>
  <button
    :class="[
      'px-4 py-2 rounded-md font-semibold text-white transition-colors duration-300 relative',
      'flex items-center justify-center min-w-[120px]',
      'bg-blue-600 hover:bg-blue-700 overflow-hidden',
    ]"
    :disabled="Number(progress) >= 100"
  >
    <span
      class="inline-block bg-blue-800 absolute inset-0"
      :style="{
        width: `${props.progress}%`,
      }"
    />
    <Transition mode="out-in">
      <span
        v-if="!done"
        class="z-10"
      >
        <slot>{{ props.label }}</slot>
      </span>

      <span
        v-else
        class="z-10"
      >
        {{ props.completeMsg || 'Completed!' }}
      </span>
    </Transition>
  </button>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: transform 0.5s;
}

.v-enter-from {
  transform: translateY(-120%);
}

.v-leave-to {
  transform: translateY(120%);
}
</style>
