<script setup lang="ts">
const links = [
  {
    name: 'Button with Loading State',
    to: '/button-with-loading',
  },
  {
    name: 'Progress Button',
    to: '/progress-button',
  },
  {
    name: 'Glow Button',
    to: '/glow-button',
  },
  {
    name: 'Glow Outline Button',
    to: '/glow-outline-button',
  },
  {
    name: 'Spotlight Button',
    to: '/spotlight-button',
  },
  {
    name: 'Material Button',
    to: '/material-button',
  },
  {
    name: 'Cursor Expand Button',
    to: '/cursor-expand-button',
  },

]
</script>

<template>
  <div>
    <h1 class="text-4xl mb-5">
      Button Showcase
    </h1>
    <ul>
      <li
        v-for="link in links"
        :key="link.to"
      >
        <NuxtLink :to="link.to">
          {{ link.name }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>
