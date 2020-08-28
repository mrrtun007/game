<template>
  <div id="app">
    <HelloWorld msg="Fighting Game"/>
    <CsButton label />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import CsButton from "./components/CSButton";
export default {
  name: "App",
  components: {
    HelloWorld,
    CsButton,
  },

  data: function () {
    return {};
  },

  methods: {},
};
</script>

<style>
#app {
  font-family: "Metal Mania", cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  background-image: url(https://thumbs.gfycat.com/ImaginativeGrandioseArcticwolf-size_restricted.gif);
  background-attachment: fixed;
  background-repeat: no-repeat;
  background-size: 100% 100%;
  height: 100vh;
}
</style>
