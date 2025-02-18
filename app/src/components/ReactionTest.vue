<template>
  <div class="game">
    <div v-if="!active" class="start">
      <div v-if="!click" class="start" @click="i++">
        <div class="height">
          <h1 class="center" v-if="!history.attempt" @click="(startGame(), (click = true))">
            Click to Start Reaction
          </h1>
          <h1 class="center" v-if="history.attempt" @click="(startGame(), (click = true))">
            Attempt:{{ history.attempt }} MS:{{ ms }}
          </h1>
        </div>
      </div>
      <div v-if="click" class="start" @click="cancel()">
        <h1>Wait for green</h1>
      </div>
    </div>

    <div class="offset" v-if="active">
      <div class="offset" v-if="!click" @click="stopGame()">
        <h1></h1>
      </div>
    </div>
  </div>
  <div class="scores">
    <h3>High Scores</h3>
    <div>
      <ul>
        <li v-for="entry in historyArray" :key="entry">
          Attempt: {{ entry.attempt }} MS: {{ entry.ms }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
let randomTime = null
let active = ref(false)
let historyArray = []
const history = reactive({ attempt: null, ms: null })
let attempt = ref(1)
let gameOver = ref(false)
// let elapsedTime = null
// let timerInterval
let ms = null
let begin = null
let end = null

let click = ref(false)
let i = 0

let startGameTimeout
// function startTimer() {
//   timerInterval = setInterval(() => {
//     elapsedTime++ // Increment elapsed time by 1ms every interval
//     console.log(elapsedTime, 'timer') // Log the elapsed time in ms
//   }, 1) // Update every 1ms
// }

// function stopTimer() {
//   clearInterval(timerInterval)
// }

function random() {
  randomTime = Math.random() * 3 + 1
}

function startGame() {
  if (gameOver.value) return
  console.log('starting')
  while (i === 0) {
    gameOver.value = false
    random()
    console.log(randomTime)
    startGameTimeout = setTimeout(() => {
      active.value = true
      begin = Date.now()
      click.value = false
      setTimeout(() => {
        gameOver.value = false
        i = 0
        attempt.value++
      }, 3000)
    }, randomTime * 1000)
    break
  }
  // if (i > 1) {
  //   console.log('too early!')
  //   gameOver.value = true
  // }
}
function stopGame() {
  end = Date.now()
  active.value = false
  ms = end - begin
  history.attempt = attempt.value
  // console.log('beginning', begin, 'ending', end)
  historyArray.push({ attempt: attempt.value, ms: ms })
  gameOver.value = false
}
function cancel() {
  console.log('canceling')
  active.value = false
  click.value = false
  clearTimeout(startGameTimeout)
  i = 0
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
