<template>
  <div class="game" @click="(missed++, console.log(randomX, randomY))">
    <button class="aim" @click="handleClick" :style="{ top: randomY + '%', left: randomX + '%' }">
      {{ clicked }}
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
let missed = ref(0)
let clicked = ref(0)
let randomX = null
let randomY = null
function handleClick() {
  clicked.value++
  randomX = Math.random() * 100
  randomY = Math.random() * 100
}
</script>

<style scoped>
.game {
  width: 85%;
  background-color: rgb(186, 255, 232);
}
.aim {
  position: relative;
  width: 1.7rem;
  height: 1.7rem;
  border-radius: 100%;
}
</style>
