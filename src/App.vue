<template>
  <HomeView />
</template>

<script>
import HomeView from "@/views/HomeView.vue";

export default {
  name: "App",
  components: { HomeView },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html,
body {
  margin: 0;
  padding: 0;
  font-family: "Nunito", sans-serif;
  font-weight: 400;
  color: #2c3e50;
  background-image: radial-gradient(#75e6da 5%, transparent 5%),
    radial-gradient(#05445e 2%, transparent 5%);
  background-color: #d4f1f4;
  background-position: 0 0, 50px 50px;
  background-size: 100px 100px;
}
#app {
  margin: 40px auto;
  width: 100%;
  max-width: 1000px;
}
</style>
