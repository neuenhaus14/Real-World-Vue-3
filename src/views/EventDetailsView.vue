
<script setup>
import { ref, onMounted } from 'vue'
import EventService from '../EventService'

const props = defineProps({
  id:{
    required: true,
  }
})

const event = ref(null)
// const id = ref(123)

onMounted(() => {
  EventService.getEvent(props.id)
  .then((response) => {
    event.value= response.data
  })
  .catch((err) => console.error(err))
})

</script>


<template >
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>
