<script setup>
import AimPractice from '@/components/AimPractice.vue'
import ReactionTest from '@/components/ReactionTest.vue'
// import { reactive } from 'vue'
// const user = reactive({ username: '', password: '' })
// function login(user) {
//   console.log(user)
// }
// const component = false
export default {
  data() {
    return {
      showComponent: true,
    }
  },
  methods: {
    toggleComponent() {
      this.showComponent = !this.showComponent
    },
  },
  components: {
    AimPractice,
    ReactionTest,
  },
}
</script>

<template>
  <div class="main">
    <div class="nav">
      <button @click="toggleComponent"><h1>Aim</h1></button>
      <button @click="toggleComponent"><h1>Reaction</h1></button>
    </div>
    <div class="center">
      <AimPractice />
      <ReactionTest />

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

<!-- <main>
  <h1>Log In</h1>
  <form action="submit" @submit.prevent="login()">
    <label for="username">Username</label>
    <input type="text" v-model="user.username" />
    <label for="password">Password</label>
    <input type="password" v-model="user.password" />
    <button type="submit">Submit</button>
  </form>
</main> -->
<template>
  <div>
    <button @click="toggleComponent">Toggle Component</button>
    <component-one v-if="showComponent" />
    <component-two v-else />
  </div>
</template>

<script setup>
import { ref } from 'vue' // Import Vue's `ref` for reactivity
import ComponentOne from '@/components/ComponentOne.vue' // Adjust the path as needed
import ComponentTwo from '@/components/ComponentTwo.vue' // Adjust the path as needed

// Define reactive state
const showComponent = ref(true)

// Define method
const toggleComponent = () => {
  showComponent.value = !showComponent.value
}
</script>
