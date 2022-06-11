<template>
  <div>
    <header></header>
    <PWAPrompt />
    <footer>
      <div class="container">Made by @gecapo</div>
    </footer>
  </div>
</template>

<script>
import PWAPrompt from "./components/PWAPrompt.vue";

export default {
  name: "App",
  components: {
    PWAPrompt,
  },
};
</script>

<style>
</style>
