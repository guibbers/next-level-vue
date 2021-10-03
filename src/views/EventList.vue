<template>
  <div>
    <h1>Events Listing</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <template v-if="page != 1">
      <router-link
        :to="{ name: 'event-list', query: { page: page - 1 } }"
        rel="prev"
        >Previous Page</router-link
      >
    </template>

    <template v-if="hasNextPage"> | </template>

    <template v-if="this.totalEvents > this.page * 3">
      <router-link
        :to="{ name: 'event-list', query: { page: page + 1 } }"
        rel="next"
        >Next Page</router-link
      >
    </template>
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
import { mapState } from 'vuex'

export default {
  components: {
    EventCard,
  },
  created() {
    this.$store.dispatch('fetchEvents', {
      perPage: 3,
      page: this.page,
    })
  },
  computed: {
    ...mapState(['events', 'totalEvents']),
    page() {
      return parseInt(this.$route.query.page) || 1
    },
    hasNextPage() {
      return this.totalEvents > this.page * this.perPage
    },
  },
}
</script>

<style></style>
