<template>
  <div class="game">
    <div v-if="!active" class="start" @click="startGame">
      <h1 class="center" v-if="!history.attempt">Click to Start Reaction</h1>
      <h1 class="center" v-if="history.attempt">
        Attempt:{{ history.attempt }} MS:{{ history.ms }}
      </h1>
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

  active.value = true

  gameOver.value = false

  setTimeout(() => {
    active.value = false

    history.attempt = attempt.value

    history.ms = ms.toFixed(1)
    historyArray.push({ attempt: history.attempt, ms: history.ms })

    attempt.value++

    gameOver.value = true
    setTimeout(() => {
      gameOver.value = false
    }, randomTime) // randomTime delay
  }, 15000)
}
</script>

<style scoped>
.game {
  width: 85%;
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
  width: 100%;
  height: 100%;
  z-index: 1;
}
</style>
