<template>
  <div class="counter">
    <svg class="progress-ring" height="120" width="120px">
      <g>
        <circle
          class="progress-ring__circle"
          stroke="grey"
          stroke-width="8"
          :stroke-dasharray="dashArray"
          :stroke-dashoffset="offset"
          fill="transparent"
          :r="radius"
          cx="60"
          cy="60"
        />
        <text x="50%" y="50%" text-anchor="middle" stroke-width="2px" dy="">
          {{ text }}
        </text>
      </g>
    </svg>
    <div>{{ title }}</div>
  </div>
</template>

<script>
export default {
  name: "CounterDown",
  props: {
    value: {
      type: Number,
      required: true,
    },
    text: {
      default() {
        return "";
      },
    },
    title: {
      default() {
        return "";
      },
    },
  },
  data() {
    return {
      radius: 52,
    };
  },

  computed: {
    circumference() {
      return this.radius * 2 * Math.PI;
    },
    dashArray() {
      return `${this.circumference} ${this.circumference}`;
    },
    offset() {
      return this.circumference - (this.value / 100) * this.circumference;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
html,
body {
  background-color: #2962ff;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  position: relative;
}

.counter {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.progress-ring__circle {
  transition: 0.35s stroke-dashoffset;
  transform: rotate(-90deg);
  transform-origin: 50% 50%;
}
</style>
