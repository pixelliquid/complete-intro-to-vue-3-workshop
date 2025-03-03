<script>
export default {
  props: ['characterList'],
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
  }
}
</script>

<template>
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