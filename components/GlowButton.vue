<script setup>
import { defineProps } from 'vue'

const btnEl = useTemplateRef('btn')

const hovering = ref(false)

const { x, y } = usePointer({
  target: btnEl,
})

const props = defineProps({
  label: {
    type: String,
    default: 'Button',
  },
})
</script>

<template>
  <button
    ref="btn"
    :class="[
      'px-4 py-2 rounded-md font-semibold text-white transition-colors duration-300 relative inline-block',
      'flex items-center justify-center min-w-[120px] overflow-hidden',
      props.loading ? 'bg-blue-400 cursor-not-allowed' : 'bg-blue-600 hover:bg-blue-700',
    ]"
    @mouseenter="hovering = true"
    @mouseleave="hovering = false"
  >
    <span
      v-if="hovering"
      class=" absolute inline-block rounded-full h-[1px] w-[1px]"
      :style="{
        left: `${x - btnEl?.offsetLeft}px`,
        top: `${y - btnEl?.offsetTop}px`,
        boxShadow: `0 0 30px 0.7rem rgba(255, 255, 255, 1)`,
        background: 'rgba(255, 255, 255, 0.55)',
      }"
    />

    <span>

      <slot>{{ props.label }}</slot>
    </span>
  </button>
</template>
