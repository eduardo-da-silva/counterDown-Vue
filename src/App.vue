<template>
  <h1>CounterDown</h1>
  <CounterDown />
</template>

<script>
import CounterDown from "./components/CounterDown.vue";

export default {
  name: "App",
  components: {
    CounterDown,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
