<template>
  <div id="app">
    <div>
      <Forecast />
    </div>
  </div>
</template>

<script>
import Forecast from "./components/Forecast.vue";

export default {
  name: "app",
  components: {
    Forecast
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #7088a0;
  margin-top: 60px;
}
p {
  font-family: "Roboto", sans-serif;
  letter-spacing: 1px;
}
</style>
