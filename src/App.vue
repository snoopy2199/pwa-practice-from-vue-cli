<template>
  <div id="app">
    <div class="header">
      PWA (Vue)
      <button v-if="promptEvent" @click="handlePromotion">install</button>
    </div>
    <HelloWorld />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'app',
  data() {
    return {
      promptEvent: null,
    };
  },
  created() {
    window.addEventListener('beforeinstallprompt', this.handleBeforeInstallPrompt);
  },
  destroyed() {
    window.removeEventListener('beforeinstallprompt', this.handleBeforeInstallPrompt);
  },
  components: {
    HelloWorld,
  },
  methods: {
    handleBeforeInstallPrompt(e) {
      this.promptEvent = e;
      console.log('beforeinstallprompt');
    },
    handlePromotion() {
      this.promptEvent.prompt();
      this.promptEvent.userChoice
        .then((choiceResult) => {
          if (choiceResult.outcome === 'accepted') {
            console.log('User accepted the A2HS prompt');
          } else {
            console.log('User dismissed the A2HS prompt');
          }
          this.promptEvent = null;
        });
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
