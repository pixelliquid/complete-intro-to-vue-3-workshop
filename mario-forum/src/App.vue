<script>
import FruitStatistics from './components/FruitStatistics.vue';
export default {
  components: {
    FruitStatistics,
  },
  data: () => ({
    newCharacter: {
      name: '',
      favs: [],
    },
    characterList: [
      {
        name: 'Mario',
        favs: ['Avocado', 'Banana', 'Orange', 'Mango'],
      },
      {
        name: 'Luigi',
        favs: ['Mango', 'Melon', 'Avocado'],
      },
      {
        name: 'Yoshi',
        favs: ['Orange', 'Pineapple', 'Raspberry'],
      },
      {
        name: 'Bowser',
        favs: ['Banana'],
      },
    ],
    favouritesList: [],
  }),
  methods: {
    addToFavourites(character) {
      this.favouritesList.push(character);
      this.characterList = this.characterList.filter(
        (char) => char.name !== character.name
      );
    },
    removeFromFavourites(favourite) {
      this.favouritesList.pop(favourite);
      this.characterList.push(favourite);
      this.favouritesList = this.favouritesList.filter(
        (char) => char.name !== character.name
      );
    },
    addCharacter() {
      this.characterList.push(this.newCharacter);
      this.newCharacter = '';
    },
  }
};
</script>

<template>
  <h1>Characters</h1>
  <ul v-if="characterList.length > 0">
    <!-- <li v-for="character in characterList" :key="character.name"> -->
    <li v-for="character in characterList" :key="character.name">
      <button @click="addToFavourites(character)">+</button>
      {{ character.name }}
    </li>
  </ul>
  <p v-else>There are no characters</p>
  <p>
    There are {{ characterList.length }} characters:
    <span v-for="(character, index) in characterList" :key="index">
      {{ character.name }}{{ index === characterList.length - 1 ? '' : ','}}
    </span>
  </p>
  <h2>Favourite characters</h2>
  <ul v-if="favouritesList.length > 0">
    <li v-for="favourite in favouritesList" :key="favourite.name">
      <button @click="removeFromFavourites(favourite)">-</button>
      {{ favourite.name }}
    </li>
  </ul>
  <p v-else>There are no favourites</p>
  <h2>Add a character</h2>
  <input
    v-model="newCharacter.name"
    @keyup.enter="addCharacter" />
  <button @click="addCharacter" :disabled="!newCharacter.name">Add Character</button>
  
  <FruitStatistics :characterList="characterList" />
</template>

<style>
  body {
    font-family: 'Inter', sans-serif;
  }
  li {
    list-style-type: none;
    margin: 1rem 0;
  }
</style>