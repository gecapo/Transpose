<template>
  <div id="app">
    <header></header>
    <PWAPrompt />
    <!-- <LiquidConverter /> -->
    <footer>
      <div class="container">Made by @gecapo</div>
    </footer>
  </div>
</template>

<script>
import PWAPrompt from "./components/PWAPrompt.vue";
// import LiquidConverter from "./components/LiquidConverter.vue";

export default {
  name: "App",
  components: {
    PWAPrompt,
    // LiquidConverter,
  },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
}
</style>
