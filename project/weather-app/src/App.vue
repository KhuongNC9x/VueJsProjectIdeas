<template>
  <Weather />
</template>

<script>
import Weather from "./components/WeatherComponent.vue";

export default {
  name: "App",
  components: {
    Weather,
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

body {
  height: 100vh;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
