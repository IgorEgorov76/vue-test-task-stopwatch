<template>
  <div class="main-block__element"
       id="element"
  >
    <div class="main-block__element-item main-block__element-item_line">
      <div v-bind:class="{text:classA}"
           class="main-block__element-item-time">{{ hours }}:{{ minutes }}:{{ sec }}</div>
    </div>
    <div class="main-block__element-item">
      <button class="main-block__element-item-button-play-pause"
              v-on:click="start"
      >
        <img v-bind:class="{img:classA}"
             src="../assets/img/main-block__element-item-button-play.svg">
        <img v-bind:class="{img:classB}"
             src="../assets/img/main-block__element-item-button-pause.svg">
      </button>
      <button class="main-block__element-item-button-reset"
              v-on:click="reset"
      >
        <img v-bind:class="{img:classA}"
             src="../assets/img/main-block__element-item-button-reset.svg">
        <img v-bind:class="{img:classB}"
             src="../assets/img/main-block__element-item-button-reset-active.svg">
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      classA: false,
      classB: true,
      pause: false,
      interval: null,
      sec: 0,
      minutes: 0,
      hours: 0,
    }
  },
  methods: {
    start() {
      if (this.pause === false) {
        this.interval = setInterval(() => this.sec = this.sec + 1, 1000)
        this.pause = true
        this.classA = !this.classA
        this.classB = !this.classB
      }
      else {
        clearInterval(this.interval)
        this.pause = false
        this.classA = !this.classA
        this.classB = !this.classB
      }
    },
    reset() {
      clearInterval(this.interval)
      this.pause = false
      this.sec = 0
      this.minutes = 0
      this.hours = 0
      this.classA = false
      this.classB = true
    }
  },
  watch: {
    sec() {
      if (this.sec > 59) {
        this.sec = 0;
        this.minutes = this.minutes + 1
      }
    },
    minutes() {
      if (this.minutes > 59) {
        this.minutes = 0;
        this.hours = this.hours + 1
      }
    }
  }
}
</script>

<style lang="scss">
.img {
  display: none;
}

.text {
  color: white;
}
</style>