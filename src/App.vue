<template>
  <div id="app">
    <img alt="Ticketty logo" src="./assets/tickettyLogo.png" />
    <Ticketty msg="Welcome to Ticketty" />
  </div>
</template>

<script>
import Ticketty from "./components/Ticketty.vue";

export default {
  name: "App",
  components: {
    Ticketty
  }
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
