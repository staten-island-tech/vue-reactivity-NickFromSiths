<template>
  <div class="game">
    <div v-if="!active" class="start" @click="startGame">
      <div class="height">
        <h1 class="center" v-if="!history.attempt">Click to Start Reaction</h1>
        <h1 class="center" v-if="history.attempt">
          Attempt:{{ history.attempt }} MS:{{ history.ms }}
        </h1>
      </div>
    </div>

    <div class="offset" v-if="active" @click=""></div>
  </div>
  <div class="scores">
    <h3>High Scores</h3>
    <div>
      <ul>
        <li v-for="entry in historyArray" :key="entry">
          Attempt: {{ entry.attempt }} Accuracy: {{ entry.accuracy }}%
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
let randomTime = null
let ms = 0
let active = ref(false)
let historyArray = []
const history = reactive({ attempt: null, ms: null })
let attempt = ref(1)
let gameOver = ref(false)

function random() {
  randomTime = Math.random() * 10
}

function startGame() {
  if (gameOver.value) return

  gameOver.value = false
  random()

  setTimeout(() => {
    active.value = true

    history.attempt = attempt.value
    history.ms = ms.toFixed(1)
    historyArray.push({ attempt: history.attempt, ms: history.ms })
    attempt.value++

    gameOver.value = true
    setTimeout(() => {
      gameOver.value = false
    }, 3000) // randomTime delay
  }, randomTime)
}
</script>

<style scoped>
.game {
  width: 85%;
}
.center {
  display: flex;
  justify-content: center;
  text-align: center;
  color: rgba(0, 189, 126, 0.57);
  height: 100%;
  align-items: center;
}
.scores {
  width: 15%;
  border-left: 1px solid var(--color-border);
  text-align: center;
}
ul {
  list-style-type: none;
  padding: 0%;
}
.start {
  position: relative;
  height: 100%;
  width: 100%;
  z-index: 11;
}
.offset {
  width: 100%;
  height: 100%;
  z-index: 1;
  background-color: rgba(0, 189, 126, 0.37);
}
.height {
  height: 100%;
}
</style>
