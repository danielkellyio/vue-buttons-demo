<script setup lang="ts">

</script>

<template>
  <NuxtLink
    to="/"
    class="absolute top-1 left-1 z-10"
  >
    <Icon
      name="fa-home"
      class="w-4 h-4"
    />
  </NuxtLink>

  <div class="h-screen flex items-center justify-center">
    <NuxtPage />
  </div>
</template>

<style>
body{
  @apply bg-slate-900 text-white;
}
</style>
