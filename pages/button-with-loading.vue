<script setup>
const loading = refAutoReset(false, 2000)
</script>

<template>
  <div>
    <h1 class="text-2xl font-semibold mb-4">
      Button with Loading
    </h1>

    <AppButton
      :loading="loading"
      @click="loading = true"
    >
      Click Me
    </AppButton>
  </div>
</template>
