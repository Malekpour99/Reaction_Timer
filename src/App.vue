<template>
  <h1>Ninja Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <Block :delay="delay" v-if="isPlaying" @end="endGame"></Block>
  <Results v-if="showResults" :score="score"></Results>
</template>

<script>
import Block from "@/components/Block.vue"
import Results from "@/components/Results.vue"

export default {
  name: 'App',
  components: {
    Block,
    Results
  },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false
    }
  },
  methods: {
    start() {
      // creating a timer between 2 seconds up to 6 seconds
      this.showResults = false
      this.delay = 2000 + Math.random() * 4000
      this.isPlaying = true
    },
    // sent data from event doesn't need to be defined in the parent component it can be accessed by default
    endGame(reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
button {
  background-color: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 1rem;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
