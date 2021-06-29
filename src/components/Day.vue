<template>
  <p>Думай головой 🤓</p>

  <p>Пиши код:</p>
  <textarea></textarea>

  <p>Кликай мышкой:</p>
  <p>{{ clickCounter }}</p>
  <button v-on:click="clickCounter++">Клик-клик</button>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'Day',

  setup() {
    const clickCounter = ref(0);

    return {
      clickCounter,
    }
  },
}
</script>

<style scoped>
textarea {
  height: 100px;
  width: 300px;
}
</style>
