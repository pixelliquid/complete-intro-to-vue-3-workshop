<script>
import BaseCounter from "./components/BaseCounter.vue";
import BaseButton from "./components/BaseButton.vue";
export default {
  components: {
    BaseCounter,
    BaseButton
  },
  data() {
    return {
      message: "Hello it works",
      listOfNumbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    };
  },
};
</script>

<template>
  <div id="app">
    <h1>Vue Playground</h1>

    <BaseCounter />
    <base-counter />

    <base-button />
    
    <hr />

    <h2 v-if="message.length % 2 === 0">
      {{ message.toUpperCase() }} (even amount of letters: {{message.length}})
    </h2>
    <h2 v-else>
      {{ message }} (uneven amount of letters: {{message.length}})
    </h2>

    <hr />
    <ul>
      <li v-for="number in listOfNumbers" :key="number">
        {{ number }}
      </li>
    </ul>
  </div>
</template>

<style>
  body {
    font-family: 'Inter', sans-serif;
  }
</style>