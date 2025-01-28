<script setup>
import { reactive } from 'vue'
const user = reactive({ username: '', password: '' })
function login(user) {
  console.log(user)
}
</script>

<template>
  <div class="main">
    <div class="top"><h1>Aim practice</h1></div>
    <div class="center">
      <div class="game"></div>
      <div class="scores">High Scores</div>
    </div>
  </div>
</template>

<style scoped>
.main {
  min-height: 40rem;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: aquamarine;
}
.top {
  padding: 1rem;
  width: 100%;
  text-align: center;
}
.center {
  width: 100%;
  flex-grow: 1; /* Allow it to grow and take available space */
  display: flex;
  flex-direction: row;
  /* align-items: stretch; Make the child elements stretch to take the full height */
}
.scores {
  width: 15%;
  background-color: rgb(67, 247, 187);
}
.game {
  width: 85%;
  background-color: rgb(67, 210, 162);
}
</style>

<!-- <main>
  <h1>Log In</h1>
  <form action="submit" @submit.prevent="login()">
    <label for="username">Username</label>
    <input type="text" v-model="user.username" />
    <label for="password">Password</label>
    <input type="password" v-model="user.password" />
    <button type="submit">Submit</button>
  </form>
</main> -->
