<template>
  <div class="main-container">
    <div class="main-block"
         id="main-block"
    >
      <new-timer v-for="timer in arrayTimers" :key="timer" />

      <div class="main-block__new-element"
           id="addBlock"
      >
        <button class="main-block__new-element-btn"
                v-on:click="addTimer"
        >
          <img src="./assets/img/main-block__new-element.svg">
        </button>
      </div>
    </div>
  </div>
</template>

<script>

import newTimer from "./components/newTimer.vue";

export default {
  components: {
    newTimer
  },

  data() {
    return {
      index: 1,
      arrayTimers: ['timer1']
    }
  },

  methods: {
    addTimer() {
      this.arrayTimers.push(`timer${this.index + 1}`);
      this.index = this.index + 1;
      console.log(this.arrayTimers)
    }
  }
}
</script>

<style lang="scss">

@font-face {
  font-family: Gotham Pro;
  src: local(Gotham Pro), url('~@/assets/fonts/gothampro.ttf') format('truetype');
}

.main-container {
  display: flex;
  justify-content: center;
  max-width: 1300px;
  margin-left: auto;
  margin-right: auto;
  background-color: #353638;
  padding-top: 72px;
  padding-bottom: 27px;
}

.main-block {
  display: flex;
  flex-wrap: wrap;
  gap: 45px 50px;
  width: 775px;

  &__element {
    display: flex;
    justify-content: center;
    flex-direction: column;
    width: 225px;
    height: 120px;
    background-color: #696969;
    color: #9E9E9E;
   }

  &__new-element {
    display: flex;
    justify-content: center;
    flex-direction: column;
    width: 225px;
    height: 120px;
    background-color: #696969;
    color: #9E9E9E;
    margin-bottom: 45px;
  }

  &__element-item {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 60px;

    &_line {
      border-bottom: 1px solid #9E9E9E;
    }
  }

  &__element-item-time {
    font-family: "Gotham Pro";
    font-size: 22px;
  }
  
  &__element-item-button-play-pause {
    margin-right: 48px;
    cursor: pointer;
    background-color: #696969;
    border: none;
  }

  &__element-item-button-reset {
    cursor: pointer;
    background-color: #696969;
    border: none;
  }

  &__new-element-btn {
    cursor: pointer;
    height: 120px;
    width: 225px;
    background-color: #696969;
    border: none;
  }
}

@media (max-width: 860px) {
  .main-block {
    width: 500px;
  }
}

@media (max-width: 580px) {
  .main-block {
    width: 225px;
  }
}
</style>
