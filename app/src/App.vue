<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'

defineProps({
  loggedIn: false,
})
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <HelloWorld msg="Vue Project" />

    <nav>
      <RouterLink v-if="loggedIn === false" to="/">Log In</RouterLink>
      <RouterLink v-if="loggedIn === false" to="/about">About</RouterLink>
      <RouterLink v-if="loggedIn === true" to="/account">Account</RouterLink>
      <RouterLink v-if="loggedIn === true" to="/about">About</RouterLink>
    </nav>
  </header>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  /* max-height: 100vh; */
}

nav {
  width: 100%;
  text-align: center;
  font-size: 1rem;
  margin-top: 2rem;
  padding: 1rem 0;
  margin-top: 1rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

/* nav a.router-link-exact-active:hover {
  background-color: var(--);
} */

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

header {
  display: flex;
  flex-direction: column;
  align-items: center;
  /* padding-right: calc(var(--section-gap) / 2); */
}

.logo {
  margin: 0;
}
</style>
