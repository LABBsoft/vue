<template>
  <Header />
  <Renderer />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
import Header from "./components/Header.vue";
import Renderer from "./components/Renderer.vue";
export default defineComponent({
  name: "App",
  components: {
    HelloWorld,
    Header,
    Renderer,
  },
});
</script>

<style lang="scss">
@import "./styles/_variables.scss";
@import url("https://fonts.googleapis.com/css2?family=Roboto");

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
}

button {
  border: 0;
  background-color: $bg-light;

  :active {
    color: lighten(black, 40%);
  }
}
</style>
