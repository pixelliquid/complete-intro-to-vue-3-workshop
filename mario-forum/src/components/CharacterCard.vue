<script>
export default {
  props: {
    character: {
      type: Object,
      required: true,
    },
  },
  emits: ['favourite'],
  methods: {
    addToFavourites() {
      this.$emit('favourite', this.character);
    },
  }
}

</script>

<template>
  <div>
    <button @click="addToFavourites">+</button>
    {{ character.name }}
  </div>
</template>

<style scoped>

</style>