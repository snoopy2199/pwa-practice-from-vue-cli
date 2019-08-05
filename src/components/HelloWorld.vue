<template>
  <div class="hello">
    {{fate}}
    <button @click="chance">抽籤</button>
    <button v-if="fate" @click="handleShare">分享</button>
    <textarea v-if="isCopyBoxShowing" :value="message" />
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      fateList: [
        '大吉', '中吉', '小吉', '吉', '末吉', '凶', '大凶',
      ],
      isCopyBoxShowing: false,
      fate: '',
    };
  },
  computed: {
    message() {
      return `我在「PWA (Vue)」(https://snoopy2199.github.io/pwa-practice-from-vue-cli/)抽到了「${this.fate}」`;
    },
  },
  methods: {
    chance() {
      this.isCopyBoxShowing = false;
      this.fate = this.fateList[Math.floor(Math.random() * this.fateList.length)];
    },
    handleShare() {
      if (navigator.share) {
        navigator.share({
          text: this.message,
        });
      } else {
        this.isCopyBoxShowing = true;
      }
    },
  },
};
</script>

<style scoped>
</style>
