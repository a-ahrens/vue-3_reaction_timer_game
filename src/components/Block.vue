<template>
  <div class="block" v-if="showBlock" @click="stopTimer">click me</div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      showBlock: false,
      timer: null,      //stores a set interval of the amount of time passed before clicking the block
      reactionTime: 0,  //updates the time taken in millisecs, updated based on rate of timer interval
    };
  },

  mounted() {
    /* 
        setTimeout() is a builtin js function used to execute a specified function
        after a specified delay in milliseconds 
    */
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },

  methods: {
    /*
        setInterval() is a builtin js function used to repeatedly call a function 
        or execute a code snippet with a fixed time delay between each call
    */
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },

    //clearInterval() is a builtin js function used to remove a specified interval
    stopTimer() {
      clearInterval(this.timer);
      this.$emit('end', this.reactionTime);
    },
  },
};
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>