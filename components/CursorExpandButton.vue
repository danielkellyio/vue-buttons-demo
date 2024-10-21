<script setup lang="ts">
import { defineProps } from 'vue'
import { customCursorKey } from './CustomCursor.vue'

const btnEl = useTemplateRef('btn')

const { setHoveringBtnData, provided } = inject(customCursorKey, {
  provided: false,
  setHoveringBtnData: () => {},
})

if (!provided) {
  throw new Error('CustomCursorButton must be use in the context of CustomCursor')
}

const hovering = ref(false)

watch(hovering, (newVal) => {
  if (newVal) {
    setHoveringBtnData({
      width: btnEl.value?.clientWidth || 0,
      height: btnEl.value?.clientHeight || 0,
      topOffset: btnEl.value?.offsetTop || 0,
      leftOffset: btnEl.value?.offsetLeft || 0,
      hovering: true,
    })
  }
  else {
    setHoveringBtnData({
      width: 0,
      height: 0,
      hovering: false,
      topOffset: 0,
      leftOffset: 0,
    })
  }
})

const props = defineProps({
  label: {
    type: String,
    default: 'Button',
  },
})

let customCursor: HTMLSpanElement | null = null

onMounted(() => {
  customCursor = document.querySelector('.custom-cursor')
  if (!customCursor) {
    customCursor = document.createElement('span')
    customCursor.classList.add('custom-cursor')
    document.body.appendChild(customCursor)
  }
})
</script>

<template>
  <button
    ref="btn"
    class="overflow-hidden relative inline-block bg-blue-800 hover:bg-blue-900 p-[2px] rounded-md"

    @mouseenter="hovering = true"
    @mouseleave="hovering = false"
  >
    <span
      :class="[
        ' z-10 relative px-4 py-2 rounded-md font-semibold text-white transition-colors duration-300 inline-block',
        'flex items-center justify-center min-w-[120px] ',
      ]"
    >

      <span>
        <slot>{{ props.label }}</slot>
      </span>
    </span>
  </button>
</template>
