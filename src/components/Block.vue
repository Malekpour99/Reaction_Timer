<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
    Click Me!
  </div>
</template>

<script>
export default {
  name: 'Block',
  props: ["delay", ],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    }
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true
      this.startTimer()
    }, this.delay)
  },
  methods: {
    startTimer() {
      // this interval will run every 10 miliseconds and add this time to the reaction time until the user clicks on the 'block' area
      this.timer = setInterval(() => {
        this.reactionTime += 10
      }, 10)
    },
    stopTimer() {
      clearInterval(this.timer)
      this.$emit('end', this.reactionTime)
    }
  }
}
</script>

<style scoped>
.block {
  width: 400px;
  border-radius: 20px;
  background-color: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>
