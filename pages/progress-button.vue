<script setup>
const progress = ref(0)

let interval

function handleClick() {
  interval = setInterval(() => {
    if (progress.value >= 100) {
      clearInterval(interval)
      progress.value = 0
      return
    }
    progress.value = progress.value + 1
  }, 25)
}

onUnmounted(() => {
  clearInterval(interval)
})
</script>

<template>
  <div>
    <h1 class="text-2xl font-semibold mb-4">
      Progress Button
    </h1>

    <ProgressButton
      :progress="progress"
      @click="handleClick"
    >
      Click Me
    </ProgressButton>
  </div>
</template>
