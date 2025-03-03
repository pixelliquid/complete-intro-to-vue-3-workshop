<script>
import BaseCounter from "./components/BaseCounter.vue";
import BaseButton from "./components/BaseButton.vue";
import UserCard from "./components/UserCard.vue";
export default {
  components: {
    BaseCounter,
    BaseButton,
    UserCard
  },
  data() {
    return {
      message: "Hello it works",
      listOfNumbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
      userData: {
        name: "Peter",
        preferredLanguage: "JavaScript",
        favouriteFood: "Sushi",
        hobbies: ["Coding", "Cooking", "Gaming"],
      },
    };
  },
  methods: {
    changeName() {
      console.log("Button clicked");
      this.userData.name = 'Snickers';
      console.log("Name changed to:", this.userData.name);
    },
  },
};
</script>

<template>
  <div id="app">
    <h1>Vue Playground</h1>

    <UserCard :user="userData" @change-name="changeName" />

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