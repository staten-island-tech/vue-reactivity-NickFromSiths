<template>
  <div class="game">
    <div class="contains">
      <div class="stats">
        <div class="stat">Accuracy: {{ ((clicked / (clicked + missed)) * 100).toFixed(1) }}%</div>
        <div class="stat">Right: {{ clicked }}</div>
        <div class="stat">Missed: {{ missed }}</div>
      </div>
      <div class="start" @click="random"></div>
      <div class="offset" @click="(missed++, console.log(randomX, randomY))">
        <button
          v-if="active"
          class="aim"
          @click="handleClick"
          :style="{ top: randomY + '%', left: randomX + '%' }"
        ></button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
let missed = ref(0)
let clicked = ref(0)
let randomX = null
let randomY = null
let active = ref(true)

function handleClick(event) {
  event.stopPropagation()
  clicked.value++
  random()
}
function random() {
  randomX = Math.random() * 100
  randomY = Math.random() * 100
}
setTimeout(() => {
  active.value = false
}, 15000)
</script>

<style scoped>
.game {
  width: 85%;
  background-color: rgb(186, 255, 232);
}
.contains {
  height: 100%;
}
.start {
  height: 100%;
  width: 100%;
  z-index: 11;
}
.stats {
  height: 1.4rem;
  display: flex;
  flex-direction: row;
  place-content: center;
}
.stat {
  margin: 0rem 2rem 0rem 2rem;
}
.aim {
  position: relative;
  width: 3rem;
  height: 3rem;
  border-radius: 100%;
  z-index: 10;
  transition: 0.5s;
}
.offset {
  margin: 0.5rem;
  width: calc(100% - 4rem);
  height: calc(100% - 5rem);
  z-index: 1;
}
</style>
