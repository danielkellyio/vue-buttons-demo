<script setup lang="ts">
const { x, y } = usePointer()
const el = useTemplateRef('el')

const hoveringBtnData = ref({ width: 0, height: 0, hovering: false, topOffset: 0, leftOffset: 0 })
const hoveringBtnDataDebounced = refDebounced(hoveringBtnData, 400)

provide(customCursorKey, {
  setHoveringBtnData: (data: { width: number, height: number, hovering: boolean }) => {
    hoveringBtnData.value = data
  },
  provided: true,
})

const style = computed(() => {
  if (!hoveringBtnData.value.hovering) {
    return {
      top: `${y.value - ((el.value?.clientHeight || 0) / 2)}px`,
      left: `${x.value - ((el.value?.clientWidth || 0) / 2)}px`,
    }
  }
  return {
    top: `${hoveringBtnData.value?.topOffset - 2}px`,
    left: `${hoveringBtnData.value?.leftOffset - 2}px`,
    width: `${hoveringBtnData.value?.width + 4}px`,
    height: `${hoveringBtnData.value?.height + 4}px`,
  }
})

onMounted(() => {
  document.body.classList.add('cursor-none')
})
onUnmounted(() => {
  document.body.classList.remove('cursor-none')
})
</script>

<script lang="ts">
export const customCursorKey = Symbol() as InjectionKey<{
  setHoveringBtnData: (data: { width: number, height: number, hovering: boolean, topOffset: number, leftOffset: number }) => void
  provided: boolean
}>
</script>

<template>
  <div>
    <slot />
    <div
      ref="el"
      :style="style"
      class="custom-cursor bg-blue-500 rounded-md w-3 h-3 fixed border border-blue-600"
      :class="{ 'hovering-btn': hoveringBtnData.hovering || hoveringBtnDataDebounced.hovering }"
    />
  </div>
</template>

<style>
.custom-cursor.hovering-btn{
  transition: all 0.4s ease;
  transform-origin:center;
}
</style>
