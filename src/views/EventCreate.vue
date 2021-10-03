<template>
  <div>
    <h1>Create event, {{ user.name }}</h1>
    <p>This event was created by the user with the id: {{ user.id }}</p>
    <p>{{ getEventById(1) }}</p>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['getEventById']),
    ...mapState(['user', 'categories']),
  },
}
</script>

<style></style>
