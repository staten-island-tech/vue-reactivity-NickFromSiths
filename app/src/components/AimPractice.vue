<template>
  <div class="game">
    <div class="contains">
      <div v-if="!active" class="start" @click="startGame">
        <h1 class="center" v-if="!history.attempt">Click to Start</h1>
        <h1 class="center" v-if="history.attempt">
          Attempt: {{ history.attempt }} Accuracy: {{ history.accuracy }}%
        </h1>
      </div>
      <div class="stats" v-if="active">
        <div class="stat">Accuracy: {{ ((clicked / (clicked + missed)) * 100).toFixed(1) }}%</div>
        <div class="stat">Right: {{ clicked }}</div>
        <div class="stat">Missed: {{ missed }}</div>
      </div>

      <div class="offset" v-if="active" @click="(missed++, console.log(randomX, randomY))">
        <button
          v-if="active"
          class="aim"
          @click="handleClick"
          :style="{ top: randomY + '%', left: randomX + '%' }"
        ></button>
      </div>
    </div>
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

let missed = ref(0)
let clicked = ref(0)
let randomX = null
let randomY = null
let active = ref(false)
let historyArray = []
const history = reactive({ attempt: null, accuracy: null }) // Null to check before game starts
let attempt = ref(1)
let gameOver = ref(false) // Prevent restart before 1 second

function handleClick(event) {
  event.stopPropagation()
  clicked.value++
  random()
}

function random() {
  randomX = Math.random() * 100
  randomY = Math.random() * 100
}

function startGame() {
  if (gameOver.value) return // Don't start a new game until 1 second after game over

  active.value = true
  random()

  // Reset stats for new game
  missed.value = 0
  clicked.value = 0
  gameOver.value = false // Reset the game over flag

  setTimeout(() => {
    active.value = false

    // Store the attempt number and accuracy when the game ends
    history.attempt = attempt.value
    history.accuracy = ((clicked.value / (clicked.value + missed.value)) * 100).toFixed(1)
    historyArray.push({ attempt: history.attempt, accuracy: history.accuracy })

    // Increment attempt for the next game
    attempt.value++

    // Set game over flag and delay before allowing another game start
    gameOver.value = true
    setTimeout(() => {
      gameOver.value = false // After 1 second, allow starting a new game
    }, 3000) // 1 second delay
  }, 15000)
}
</script>

<style scoped>
.game {
  width: 85%;
}
.contains {
  height: 100%;
  position: relative;
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
  border: 0;
  position: relative;
  width: 3rem;
  height: 3rem;
  border-radius: 100%;
  z-index: 10;
  transition: 0.3s;
  background-color: rgba(0, 189, 126, 0.37);
}
.offset {
  margin: 0.5rem;
  width: calc(100% - 4rem);
  height: calc(100% - 5rem);
  z-index: 1;
}
</style>
