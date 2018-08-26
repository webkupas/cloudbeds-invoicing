<template>
  <div id="app">
    <Invoice/>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld";
import Invoice from "./components/Invoice";

export default {
  name: "App",
  components: {
    Invoice
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
