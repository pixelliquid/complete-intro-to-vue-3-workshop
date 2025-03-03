<script>
export default {
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
  computed: {
    // solution copilot:
    favStatistics() {
      const stats = {};
      this.characterList.forEach(character => {
        character.favs.forEach(fav => {
          if (!stats[fav]) {
            stats[fav] = { count:0, names:[]};
          }
          stats[fav].count++;
          stats[fav].names.push(character.name);
        });
      });
      return stats;
    },
    // solution Ben:
    favStatisticsFixed() {
      const favs = ['Avocado', 'Banana', 'Orange', 'Mango', 'Melon', 'Pineapple'];
      const stats = {
        Avocado: 0,
        Banana: 0,
        Orange: 0,
        Mango: 0,
        Melon: 0,
        Pineapple: 0
      };

      this.characterList.forEach((character) => {
        favs.forEach((fav) => {
          if (character.favs.includes(fav)) {
            stats[fav]++;
          }
        });
      });
      return stats;
    }
  },
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
  <h2>Statistics – fav fruits:</h2>
  <pre>solution Ben (fixed array):</pre>
  <!-- <pre>{{ favStatisticsFixed}}</pre> -->
  <ul>
    <!-- <li v-for="stat in favStatisticsFixed"> only shows value -->
    <li v-for="(stat, fruit) in favStatisticsFixed" :key="`character-${stat}-${fruit}`">
      {{ fruit }} is fav by {{ stat }}
    </li>
  </ul>
  <pre>solution copilot (dynamic array):</pre>
  <!-- <pre>{{ favStatistics}}</pre> -->
  <ul>
    <li v-for="(data, fruit) in favStatistics" :key="fruit">
      {{ fruit }} is fav by {{ data.count }}: <span v-for="(name, index) in data.names" :key="name">{{ name }}{{ index === data.names.length - 1 ? '' : ', ' }}</span>
    </li>
  </ul>
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