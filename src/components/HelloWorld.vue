<script setup lang="ts">
import { Ref, ref } from 'vue'
import axios from 'axios'

defineProps<{ msg: string }>()

const loginData: Ref<string|null> = ref(null)
const error: Ref<string|null> = ref(null)

const login = () => {
  error.value = null
  axios({
    url: 'http://localhost:3000/api/nscalealinst1/graphql',
    method: 'post',
    data: {
      query: `
        query sessionInfo {
          authenticationService {
            login {
              sessionPrincipalId
              sessionPrincipal {
                userName
                domainName
              }
              sessionGroupIds
              sessionDefaultPositionId
              sessionPositionIds
              serverVersion
            }
          }
        }
        `
      }
    }
  ).then((result) => {
    loginData.value = result.data
  }).catch((err) => {
    error.value = err.message
  });
}

const logout = () => {
  axios({
    url: 'http://localhost:3000/api/nscalealinst1/graphql',
    method: 'post',
    data: {
      query: `
        mutation sessionLogout {
          AuthenticationService_logout
        }
        `
      }
    }
  ).then((result) => {
    loginData.value = null
    error.value = null
  }).catch((err) => {
    error.value = err.message
  });
  
}

</script>

<template>

  <div class="flex flex-col gap-4 w-full h-full justify-center items-center">
    
    <h1 class="dark-world">{{msg}}</h1>

    <div class="flex flex-col gap-4 border rounded-lg h-5/6 w-11/12 md:w-1/3 md:h-1/3 p-4">
      <header class="flex gap-4 justify-between">
        <a href="http://localhost:8080/res/graphql-ref.html#_login" target="_blank">nscale GraphQL</a>
        <button v-if="!loginData" class="border px-4 py-2 rounded" type="button" @click="login">Login</button>
        <button v-if="loginData" class="border px-4 py-2 rounded" type="button" @click="logout">Logout</button>
      </header>
      <main class="flex flex-col justify-center items-center h-full overflow-auto">
        <textarea class="dark-world w-full h-full" v-if="loginData" :value="JSON.stringify(loginData, null, 4)"></textarea>
        <p v-if="!loginData">Nicht angemeldet</p>
        <p v-if="error" class="text-red-500">{{error}}</p>
      </main>
    </div>
    
  </div>

</template>

<style scoped>
</style>
