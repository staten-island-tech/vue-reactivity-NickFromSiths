<script setup>
import { reactive } from 'vue'
const user = reactive({ username: '', password: '' })
function login(user) {
  console.log(user)
}
</script>

<template>
  <main>
    <h1>Log In</h1>
    <form action="submit" @submit.prevent="login()">
      <label for="username">Username</label>
      <input type="text" v-model="user.username" />
      <label for="password">Password</label>
      <input type="password" v-model="user.password" />
      <button type="submit">Submit</button>
    </form>
  </main>
</template>
