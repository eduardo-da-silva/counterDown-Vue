<template>
  <input v-model="date" type="date" min="0" max="100" placeholder="progress" />
  <div class="remaingTime">
    <Circle :value="(days / 24) * 100" :text="days" title="Days" />
    <Circle :value="(hours / 24) * 100" :text="hours" title="Hours" />
    <Circle :value="(minutes / 60) * 100" :text="minutes" title="Minutes" />
    <Circle :value="(seconds / 60) * 100" :text="seconds" title="Seconds" />
  </div>
</template>

<script>
import { defineAsyncComponent } from 'vue';
const Circle = defineAsyncComponent(() => import('./Circle.vue'));

export default {
  name: 'CounterDown',
  components: {
    Circle,
  },
  data() {
    return {
      date: '2023-12-25',
      initialDays: null,
      days: null,
      hours: null,
      minutes: null,
      seconds: null,
      intervalId: null,
    };
  },
  methods: {
    calcRemaining() {
      const currentDate = new Date();
      const finalDate = new Date(this.date);
      let remainingTime = Math.abs(finalDate - currentDate);
      this.days = Math.floor(remainingTime / (1000 * 60 * 60 * 24));
      remainingTime -= this.days * 1000 * 60 * 60 * 24;
      this.hours = Math.floor(remainingTime / (1000 * 60 * 60));
      remainingTime -= this.hours * 1000 * 60 * 60;
      this.minutes = Math.floor(remainingTime / (1000 * 60));
      remainingTime -= this.minutes * 1000 * 60;
      this.seconds = Math.floor(remainingTime / 1000);
    },
  },
  created() {
    this.intervalId = setInterval(() => this.calcRemaining(), 1000);
    const currentDate = new Date();
    let remainingTime = Math.abs(this.date - currentDate);
    this.initialDays = Math.floor(remainingTime / (1000 * 60 * 60 * 24));
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
/* input {
  position: fixed;
  top: 10px;
  left: 10px;
  width: 180px;
} */
.remaingTime {
  margin-top: 20px;
  display: flex;
  justify-content: center;
}
</style>
