<template>
  <div id="app">
    <div class="header">
      PWA (Vue)
      <button v-if="promptEvent" @click="handlePromotion">安裝</button>
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
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.header {
  background-color: #FFAB73;
  color: #3C3C3C;
  height: 40px;
  line-height: 40px;
  font-size: 18px;
  position: relative;
}

button {
  width: 70px;
  border-radius: 5px;
  padding: 3px;
  border: none;
  outline: none;
}

.header button {
  background-color: #ffffff;
  position: absolute;
  right: 20px;
  top: 8px;
}
</style>
