<template>
  <div id="app">
    <LayoutApp />
  </div>
</template>

<script>
import LayoutApp from "./views/LayoutApp.vue";

export default {
  name: "App",
  components: {
    LayoutApp,
  },
};
</script>

<style>
@import url("../src/style/reset.css");
@import url("https://fonts.googleapis.com/css2?family=Livvic:wght@400;700&family=Poppins:ital@0;1&display=swap");
#app {
  font-family: Poppins, Helvetica, sans-serif;
  float: left;
  position: fixed;
  z-index: 0;
  background-color: #c8c8c8;
  width: 100vw;
  height: 100vh;
}
</style>
