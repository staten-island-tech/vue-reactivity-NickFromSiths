<script setup>
import AimPractice from '@/components/AimPractice.vue'
import ReactionTest from '@/components/ReactionTest.vue'

// const toggle = true
// const togle = false
//@click="toggle = !toggle"
</script>

<template>
  <div class="main">
    <div class="nav">
      <button><h3>Aim Test</h3></button>
      <button><h3>Reaction Test</h3></button>
    </div>
    <div class="center">
      <AimPractice />
      <ReactionTest v-if="togle" />
      <div class="scores">High Scores</div>
    </div>
  </div>
</template>

<style scoped>
.nav {
  width: 100%;
  text-align: center;
  font-size: 1rem;
  padding: 1rem 0;
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
  background-color: rgb(0, 189, 126);
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
</style>
