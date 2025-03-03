<script>
export default {
  data() {
    return {
      count: 10,
      counterTitle: "Counter",
      incrementAmount: 10,
    };
  },
  computed: {
    displayTitle() {
      if (this.count > 20) {
        return "Counter is soo high!";
      } else {
        return "Counter";
      }
    }
  },
  methods: {
    changeIncrementAmount(event) {
      console.log(event.target.value)
      // this.incrementAmount = event.target.value - this will not work as its a string
      this.incrementAmount = Number(event.target.value) // we have to convert this to number
    },
    incrementCount() {
      this.count += this.incrementAmount;
    },
    decrementCount() {
      this.count -= this.incrementAmount;
    },
  },
  watch: {
    count(newValue) {
      console.log("count changed to", newValue);
      if (newValue > 20) {
        this.counterTitle += " is soo high!";
      }
    }
  },
};
</script>

<template>
  <h2>Counter</h2>
  <p>{{ displayTitle }}: {{ count }}</p>
    <div class="counterTools">
      <button v-on:click="incrementCount">Increment count</button>
      <button @click="decrementCount">Decrement count</button>
      <label for="incrementCount">Increment by:</label>
      <!-- using v-model -->
      <input
        type="number"
        id="incrementCount"
        v-model="incrementAmount"
      />
      <!-- without v-model -->
      <input type="number" id="incrementCount" v-bind:value="incrementAmount" v-on:input="changeIncrementAmount" />
    </div>
</template>

<style scoped>
  .counterTools {
    display: flex;
    gap: 1rem;
  }
</style>