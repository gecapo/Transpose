<template>
  <transition name="fade-up-in" appear>
    <div v-if="shown" class="pwa-prompt" :class="[{ shown }]">
      Add app to home screen?

      <button class="install-button" @click="installPWA">Install!</button>

      <button class="close-button" @click="dismissPrompt">
        <span aria-hidden="true">×</span>
        <span class="sr">Dismiss without installing</span>
      </button>
    </div>
  </transition>
</template>


<script>
export default {
  data: () => ({
    installEvent: undefined,
    shown: false,
  }),
  beforeMount() {
    window.addEventListener("beforeinstallprompt", (e) => {
      e.preventDefault();
      this.installEvent = e;
      this.shown = true;
    });
  },
  methods: {
    installPWA() {
      this.installEvent.prompt();
      this.installEvent.userChoice.then(() => {
        this.dismissPrompt();
      });
    },
    dismissPrompt() {
      this.shown = false;
    },
  },
};
</script>


<style>
</style>