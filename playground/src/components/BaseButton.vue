<script>
export default {
  data() {
    return {
      count: 16,
    };
  },
  methods: {
    increaseFontsize() {
      this.count += 1;
    },
    decreaseFontsize() {
      this.count -= 1;
    },
  },
  watch: {
    count(newValue) {
      document.body.style.fontSize = `${newValue}px`;
    },
  },
}
</script>

<template>
  <h2>Fontsizer</h2>
  <button @click="increaseFontsize()">+</button>
  {{ count }}
  <button @click="decreaseFontsize()">-</button>
</template>

<style scoped>

</style>