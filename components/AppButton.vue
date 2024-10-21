<script setup lang="ts">
import { defineProps } from 'vue'

const props = defineProps<{
  loading?: boolean
  label?: string
}>()
</script>

<template>
  <button
    :class="[
      'px-4 py-2 rounded-md font-semibold text-white transition-colors duration-300',
      'flex items-center justify-center min-w-[120px]',
      props.loading ? 'bg-blue-400 cursor-not-allowed' : 'bg-blue-600 hover:bg-blue-700',
    ]"
    :disabled="props.loading"
  >
    <span
      v-if="props.loading"
      class="mr-2"
    >
      <svg
        class="animate-spin h-5 w-5 text-white"
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
      >
        <circle
          class="opacity-25"
          cx="12"
          cy="12"
          r="10"
          stroke="currentColor"
          stroke-width="4"
        />
        <path
          class="opacity-75"
          fill="currentColor"
          d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
        />
      </svg>
    </span>
    <span>
      <slot>{{ props.label }}</slot>
    </span>
  </button>
</template>
