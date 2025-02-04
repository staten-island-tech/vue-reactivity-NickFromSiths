<template>
  <div class="game" @click="missed++">
    <button class="aim">{{ missed }}</button>
  </div>
</template>

<script setup>
const missed = 0
const randomX = Math.random() * 100
const randomY = Math.random() * 100
</script>

<style scoped>
.game {
  width: 85%;
  background-color: rgb(186, 255, 232);
}
.aim {
  position: absolute;
  top: randomX;
  left: randomY;
  width: 1.7rem;
  height: 1.7rem;
  border-radius: 100%;
}
</style>
