<script setup lang="ts">
import { defineProps } from 'vue'

const props = defineProps<{
  loading?: boolean
  label?: string
}>()

const btnEl = useTemplateRef('btnEl')
const { x, y } = usePointer()
const clicked = refAutoReset({ x: 0, y: 0 }, 500)
</script>

<template>
  <button
    ref="btnEl"
    :class="[
      'px-4 py-2 rounded-md font-semibold text-white transition-colors duration-300',
      'flex items-center justify-center min-w-[120px] overflow-hidden relative',
      'bg-blue-600 hover:bg-blue-700',
    ]"
    @click="clicked = { x: x - (btnEl?.offsetLeft || 0), y: y - (btnEl?.offsetTop || 0) }"
  >
    <span
      v-if="clicked.x && clicked.y"

      class="bg-black opacity-20 expand rounded-full w-5 h-5 absolute"
      :style="{ top: `${clicked.y}px`, left: `${clicked.x}px` }"
    />
    <span>
      <slot>{{ props.label }}</slot>
    </span>
  </button>
</template>

<style scoped>
@keyframes expand{
    from{
        transform: scale(0);
        opacity:.5;
    }
    to{
        transform: scale(5);
        opacity: 0;
    }
}

.expand{
    animation: expand 0.5s ease-out;
}
</style>
