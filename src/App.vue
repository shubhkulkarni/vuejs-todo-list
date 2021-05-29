<template>
  <div class="appContainer">
    <Hero />
  </div>
</template>

<script>
import Hero from "./components/Hero";
export default {
  name: "App",
  data() {
    return {
      name: "Shubham",
    };
  },
  components: {
    Hero,
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
}
html {
  box-sizing: border-box;
}
.appContainer {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #2c3e50;
}
body {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}
</style>
