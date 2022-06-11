<template>
  <div id="app">
    <header></header>
    <PWAPrompt />
    <nav>
      <SimpleRouter />
    </nav>
    <footer>
      <div class="container">Made by @gecapo</div>
    </footer>
  </div>
</template>

<script>
import SimpleRouter from "@/components/SimpleRouter";

export default {
  name: "App",
  components: { SimpleRouter },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
}
</style>
