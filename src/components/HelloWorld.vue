<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0)
</script>

<template>

  <div class="flex w-full h-full justify-center items-center">
    <h1 class="dark-world">{{msg}}</h1>
  </div>

</template>

<style scoped>
</style>
