<script setup>
import AimPractice from '@/components/AimPractice.vue'
import ReactionTest from '@/components/ReactionTest.vue'
import { ref } from 'vue'
const toggle = ref(true)
const togle = ref(false)
//@click="toggle = !toggle"
</script>

<template>
  <div class="main">
    <nav>
      <a @click="((toggle = true), (togle = false))"><h3>Aim Test</h3></a>
      <a @click="((toggle = false), (togle = true))"><h3>Reaction Test</h3></a>
    </nav>
    <div class="center">
      <AimPractice v-if="toggle" />
      <ReactionTest v-if="togle" />
    </div>
  </div>
</template>

<style scoped>
a:hover {
  cursor: pointer;
}
nav a.active {
  color: var(--color-text);
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
  width: 13%;
}

nav a:first-of-type {
  border: 0;
}

nav {
  width: 100%;
  text-align: center;
  font-size: 1rem;
  padding: 1rem 0;
  border-bottom: 1px solid var(--color-border);
}
.top {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
  background: none;
  border: none;
  outline: none;
  width: 200px;
  text-align: center;
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
  background-color: rgba(0, 189, 126, 0.11);
}

.center {
  width: 100%;
  flex-grow: 1; /* Allow it to grow and take available space */
  display: flex;
  flex-direction: row;
  /* align-items: stretch; Make the child elements stretch to take the full height */
}
</style>
