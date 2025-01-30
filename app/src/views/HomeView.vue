<script setup>
import { reactive } from 'vue'
const user = reactive({ username: '', password: '' })
function login(user) {
  console.log(user)
}
</script>

<template>
  <div class="main">
    <div class="nav">
      <div class="top"><h1>Aim practice</h1></div>
      <div class="top"><h1>Reaction test</h1></div>
    </div>
    <div class="center">
      <div class="game"></div>
      <div class="scores">High Scores</div>
    </div>
  </div>
</template>

<style scoped>
.nav {
  display: flex;
  flex-direction: row;
}
.nav.top {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

.nav.top:first-of-type {
  border: 0;
}

.main {
  min-height: 40rem;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(0, 189, 126);
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
  background-color: rgb(186, 255, 232);
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
