<template>
  <div class="main-block__element"
       :class="`main-block__element_${currentState}`"
  >
    <div class="main-block__element-item main-block__element-item_line">
      <div class="main-block__element-item-time">{{ hours }}:{{ minutes }}:{{ sec }}</div>
    </div>
    <div class="main-block__element-item">
      <button v-if="currentState === 'pause' || currentState === 'reset'" @click="start" class="main-block__element-item-button-play">
        <img src="../assets/img/main-block__element-item-button-play.svg">
      </button>
      <button v-else @click="pause" class="main-block__element-item-button-pause">
        <img src="../assets/img/main-block__element-item-button-pause.svg">
      </button>
      <button @click="reset" class="main-block__element-item-button-reset">
        <img v-if="currentState === 'reset' || currentState === 'pause'" src="../assets/img/main-block__element-item-button-reset.svg">
        <img v-else src="../assets/img/main-block__element-item-button-reset-active.svg">
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      interval: null,
      time: 0,
      isActive: false
    }
  },

  computed: {
    sec() {
      return this.time % 60
    },
    minutes() {
      return parseInt(this.time / 60, 10) % 60
    },
    hours() {
      return parseInt(this.time / 3600, 10)
    },
    currentState() {
      if (this.time === 0) {
        return 'reset'
      } else {
        if (this.isActive) {
          return 'play'
        } else {
          return 'pause'
        }
      }
    }
  },

  methods: {
    start() {
      this.isActive = true;
      this.interval = setInterval(() => this.time = this.time + 1, 1000)
    },
    pause() {
      this.isActive = false;
      clearInterval(this.interval)
    },
    reset() {
      this.isActive = false;
      clearInterval(this.interval);
      this.time = 0
    }
  }
}
</script>

<style lang="scss">
.main-block {
  &__element {
    &_play {
      .main-block__element-item-time {
        color: white;
      }
    }
  }
}
</style>