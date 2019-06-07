<template>
  <section class="center">
    <button class="button is-primary" @click="somethingHappends">{{ buttonDefault }}</button>
  </section>
</template>

<script>
export default {
  data() {
    return {
      buttonDefault: 'Start a new session',
      productive: [],
      newTime: null,
      savedTime: null,
    };
  },
  mounted() {
    if (localStorage.buttonDefault) {
      this.buttonDefault = localStorage.buttonDefault;
    }
    if (localStorage.savedTime) {
      this.savedTime = localStorage.savedTime;
    }
    if (localStorage.getItem('productive')) {
      try {
        this.productive = JSON.parse(localStorage.getItem('productive'));
      } catch (e) {
        localStorage.removeItem('productive');
      }
    }
  },
  methods: {
    addTime() {
      const DATE = new Date();
      const timestamp = Number(DATE);
      localStorage.setItem('timestamp', timestamp);

      // if (!this.newTime) {
      //   return;
      // }
      // this.productive.push(this.newTime);
      // this.savedTime = this.newTime;
      // this.newTime = '';
      // this.saveTime();
    },
    removeTime(x) {
      this.productive.splice(x, 1);
      this.saveTime();
    },
    saveTime() {
      const parsed = JSON.stringify(this.productive);
      localStorage.setItem('productive', parsed);
    },
    somethingHappends() {
      if (this.buttonDefault === 'Start a new session') {
        this.buttonDefault = 'Stop session';
        this.addTime();
      } else if (this.buttonDefault === 'Stop session') {
        const timestamp = localStorage.getItem('timestamp');
        const date = new Date(Number(timestamp));
        const timestampA = date;
        const timestampB = new Date().getTime();
        const difference = timestampB - timestampA;
        this.buttonDefault = 'Start a new session';
        // eslint-disable-next-line
        console.log(difference);
      }
    },
  },
};
</script>

<style>
.center {
  text-align: center;
}
</style>
