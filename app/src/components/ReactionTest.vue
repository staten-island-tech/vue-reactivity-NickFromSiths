<template>
  <div class="game">
    <div v-if="!active" class="start" @click="(startGame(), i++, console.log(i))">
      <div class="height">
        <h1 class="center" v-if="!history.attempt">Click to Start Reaction</h1>
        <h1 class="center" v-if="history.attempt">
          Attempt:{{ history.attempt }} MS:{{ history.ms }}
        </h1>
      </div>
    </div>

    <div class="offset" v-if="active" @click="(stopTimer, (active = false))">
      <h1>{{ elapsedTime }}</h1>
    </div>
  </div>
  <div class="scores">
    <h3>High Scores</h3>
    <div>
      <ul>
        <li v-for="entry in historyArray" :key="entry">
          Attempt: {{ entry.attempt }} MS: {{ entry.accuracy }}%
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
let randomTime = null
let ms = ref(0)
let active = ref(false)
let historyArray = []
const history = reactive({ attempt: null, ms: null })
let attempt = ref(1)
let gameOver = ref(false)
let elapsedTime = ref(0)
let timerInterval
let i = ref(0)

function startTimer() {
  timerInterval = setInterval(() => {
    elapsedTime++ // Increment elapsed time by 1ms every interval
    console.log(elapsedTime, 'timer') // Log the elapsed time in ms
  }, 1) // Update every 1ms
}

function stopTimer() {
  clearInterval(timerInterval)
}

function random() {
  randomTime = Math.random() * 7
}

function startGame() {
  console.log('WHY')
  if (gameOver.value && i === 1) return

  gameOver.value = false
  random()
  console.log(randomTime)
  setTimeout(() => {
    startTimer()

    active.value = true

    history.attempt = attempt.value
    history.ms = ms.toFixed(1)
    historyArray.push({ attempt: history.attempt, ms: history.ms })
    attempt.value++

    gameOver.value = true
    setTimeout(() => {
      gameOver.value = false
      i = 0
    }, 3000)
  }, randomTime * 1000)
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
