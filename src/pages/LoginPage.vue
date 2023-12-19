<script setup lang="ts">
import { ref } from 'vue'

interface LoginData {
  username: string
  password: string
}

const loginData = ref<LoginData>({
  username: '',
  password: ''
})

const loginresult = ref<string>('')

const login = async () => {
  const res = await fetch('/api/login', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(loginData.value)
  })

  if (!res.ok) {
    loginresult.value = "Failed to login"
  }else{
    loginresult.value = "Success"
  }

}


</script>
<template>
  <h2> Login form</h2>
  <div>
    <label>UserName </label>
    <input v-model="loginData.username" type="text" />
  </div>
  <div>
    <label>Pass </label>
    <input v-model="loginData.password" type="password" />
  </div>
  <div><button @click="login">Login</button></div>
  <div>{{ loginresult }}</div>
</template>

