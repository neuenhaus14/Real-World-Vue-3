<script setup>
import EventCard from '@/components/EventCard.vue'
import EventService from '../EventService';
import ContactForm from '../components/ContactForm.vue'
import AboutView from './AboutView.vue'

import { ref, onMounted } from 'vue'

const events = ref(null)

onMounted(() => {
  EventService.getEvents()
  .then((response) => {
    events.value= response.data
  })
  .catch((err) => console.error(err))

})

</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <AboutView />
    <ContactForm />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
