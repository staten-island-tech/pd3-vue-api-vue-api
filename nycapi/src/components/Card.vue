<template>
  <router-link :to="path" class="card">
    <h2>{{ request.complaint_type }}</h2>
    <p>Description: {{ request.descriptor }}</p>
    <p>Called {{ request.agency_name }}, {{ request.agency }}</p>
    <p>Address: {{ request.incident_address }}, {{ request.incident_zip }}</p>
    <p v-if="request.status === 'Closed'">Date Closed: {{ request.closed_date }}</p>
    <p v-else>Date Created: {{ request.created_date }}</p>
    <p>Borough: {{ request.borough }}</p>
    <p>Status: {{ request.status }}</p>
  </router-link>
  <!-- updated date -->
</template>

<script setup>
import {computed} from 'vue'
const props = defineProps({
  request: Object,
  id: Number
})
const path = computed(()=>{return `/Data/${props.request}`})
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  width: 27vw;
  height: 65vh;
  margin: 1rem auto;
  align-items: center;
  background-color: var(--secondary);
  border: solid;
  border-radius: 1rem;
  border: 1px solid;
  color: var(--inv);
  box-shadow: var(--shadow) 0px 3px 8px;
}
</style>
