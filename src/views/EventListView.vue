<script setup>
import EventCard from '@/components/EventCard.vue'
import { ref, onMounted } from 'vue'
import EventService from "@/services/EventService"

const events = ref(null)

onMounted(async () => {
  const response = await EventService.getEvents()
  events.value = response.data
})
</script>

<template>
  <div class="events">
    <h1>Events for Good</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
