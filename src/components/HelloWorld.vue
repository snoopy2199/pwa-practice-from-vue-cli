<template>
  <div class="hello">
    <div class="fate">{{fate}}</div>
    <div>
      <button @click="chance">抽籤</button>
      <button v-if="fate" @click="handleShare">分享</button>
    </div>
    <textarea v-if="isCopyBoxShowing" :value="message" class="share-text" />
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
.hello {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.hello button {
  background-color: #FFAB73;
  margin: 10px;
  font-size: 14px;
}

.fate {
  font-size: 80px;
  margin: 20px;
  height: 100px;
}

.share-text {
  width: 60%;
  border-radius: 5px;
  border: solid #bbbbbb 1px;
  height: 36px;
  line-height: 36px;
  padding: 0 10px;
  margin-top: 20px;
  outline: none;
}
</style>
