<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <HelloWorld msg="nappl-Login mit Vue via GraphQL" />
</template>

<style>
html, body, #app {
  @apply w-full h-full
}
body, .dark-world {
  @apply dark:bg-neutral-800 dark:text-neutral-100
}

</style>
