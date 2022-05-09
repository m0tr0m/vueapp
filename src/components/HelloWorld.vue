<script setup lang="ts">
import { Ref, ref } from 'vue'

defineProps<{ msg: string }>()


const loginData: Ref<string|null> = ref('Nicht angemeldet')

const login = () => {
  loginData.value = 'Du bist angemeldet'
}

const logout = () => {
  loginData.value = 'Nicht angemeldet'
}

</script>

<template>

  <div class="flex flex-col gap-4 w-full h-full justify-center items-center">
    
    <h1 class="dark-world">{{msg}}</h1>

    <div class="flex flex-col gap-4 border rounded-lg h-5/6 w-11/12 md:w-1/3 md:h-1/3 p-4">
      <header class="flex gap-4 justify-end">
        <button class="border px-4 py-2 rounded hover:bg-neutral-300 hover:text-black" type="button" @click="login">
          Login
        </button>
        <button class="border px-4 py-2 rounded hover:bg-neutral-300 hover:text-black" type="button" @click="logout">
          Logout
        </button>
      </header>
      <main class="flex justify-center items-center h-full overflow-auto">
        <textarea class="dark-world w-full h-full" v-if="loginData" 
          :value="loginData"></textarea>
      </main>
    </div>
    
  </div>

</template>

<style scoped>
</style>
