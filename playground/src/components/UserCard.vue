<script>
export default {
  props:{
    user: {
      type: Object,
      required: true
    },
  },
  emits: ['change-name']
}
</script>

<template>
  <div class="user-card">
    <h2>User: {{ user.name }}</h2><!-- only referencing one prop -->
    <p>Favourite food: {{ user.favouriteFood }}</p><!-- referencing user object -->
    <button @click="$emit('change-name')">Change now</button>
  </div>
</template>