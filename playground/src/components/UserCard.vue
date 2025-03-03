<script>
export default {
  props:{
    user: {
      type: Object,
      required: true
    },
    name: {
      type: String,
      default: 'Snickers'
    },
  },
}
</script>

<template>
  <div class="user-card">
    <h2>User: {{ name }}</h2><!-- only referencing one prop -->
    <p>Favourite food: {{ user.favouriteFood }}</p><!-- referencing user object -->
  </div>
</template>