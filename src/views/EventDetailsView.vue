<script setup>
import { ref, onMounted } from 'vue'
import EventService from "@/services/EventService"

const event = ref(null)

const props = defineProps({
  id: {
    type: Number,
    required: true,
  },
})

onMounted(async () => {
  const response = await EventService.getEvent(props.id)
  event.value = response.data
})
</script>

<template>
  <div class="event-card-details-view" v-if="event">
    <div class="event-card-details">
      <h2>{{ event.title }}</h2>
      <p>{{ event.time }} on {{ event.date }} @ {{ event.location}}</p>
      <p>{{ event.description }}</p>
    </div>
  </div>
</template>
<style scoped>
.event-card-details-view {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.event-card-details {
  padding: 20px;
  width: 350px;
  cursor: pointer;
  margin-bottom: 18px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>