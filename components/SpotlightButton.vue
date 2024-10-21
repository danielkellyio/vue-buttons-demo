<script setup>
import { ref, computed } from 'vue'

const btnEl = ref(null)

const hovering = ref(false)

const mousePos = ref({ x: 0, y: 0 })

const props = defineProps({
  label: {
    type: String,
    default: 'Button',
  },
  loading: {
    type: Boolean,
    default: false,
  },
})

const updateMousePosition = (event) => {
  if (btnEl.value) {
    const rect = btnEl.value.getBoundingClientRect()
    mousePos.value = {
      x: event.clientX - rect.left,
      y: event.clientY - rect.top,
    }
  }
}

const spotlight1Style = computed(() => ({
  left: `${mousePos.value.x}px`,
  top: `${mousePos.value.y}px`,
  background: 'radial-gradient(circle, rgba(255,255,255,0.2) 0%, rgba(255,255,255,0) 70%)',
  boxShadow: '0 0 15px 5px rgba(255,255,255,0.1)',
  transform: 'translate(-50%, -50%) scale(1.2)',
}))

const spotlight2Style = computed(() => ({
  left: `${btnEl.value ? btnEl.value.offsetWidth - mousePos.value.x : 0}px`,
  top: `${btnEl.value ? btnEl.value.offsetHeight - mousePos.value.y : 0}px`,
  background: 'radial-gradient(circle, rgba(255,255,255,0.15) 0%, rgba(255,255,255,0) 70%)',
  boxShadow: '0 0 15px 5px rgba(255,255,255,0.08)',
  transform: 'translate(-50%, -50%) scale(0.8)',
}))
</script>

<template>
  <button
    ref="btnEl"
    :class="[
      'px-4 py-2 rounded-md font-semibold text-white transition-colors duration-300 relative inline-block',
      'flex items-center justify-center min-w-[120px] overflow-hidden',
      props.loading ? 'bg-blue-400 cursor-not-allowed' : 'bg-blue-600 hover:bg-blue-700',
    ]"
    @mouseenter="hovering = true"
    @mouseleave="hovering = false"
    @mousemove="updateMousePosition"
  >
    <span
      v-if="hovering"
      class="absolute inline-block rounded-full h-20 w-20 pointer-events-none"
      :style="spotlight1Style"
    />
    <span
      v-if="hovering"
      class="absolute inline-block rounded-full h-16 w-16 pointer-events-none"
      :style="spotlight2Style"
    />
    <span class="relative z-10">
      <slot>{{ props.label }}</slot>
    </span>
  </button>
</template>
