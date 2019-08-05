<template>
  <div class="hello">
    <button @click="handleShare">share</button>
    <input v-if="isCopyBoxShowing" type="text" value="Hello World!" />
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      isCopyBoxShowing: false,
    };
  },
  methods: {
    handleShare() {
      if (navigator.share) {
        navigator.share({
          text: 'Hello World!',
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
