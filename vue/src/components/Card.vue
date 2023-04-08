<template>
  <div class="card">
    <h2>{{ request.complaint_type }}</h2>
    <p>Description: {{ request.descriptor }}</p>
    <p>Called {{ request.agency_name }}, {{ request.agency }}</p>
    <p>Address: {{ request.incident_address }}, {{ request.incident_zip }}</p>
    <p v-if="request.status === 'Closed'">Date Closed: {{ request.closed_date }}</p>
    <p v-else>Date Created: {{ request.created_date }}</p>
    <p>Borough: {{ request.borough }}</p>
    <p>Status: {{ request.status }}</p>
  </div>
</template>

<script setup>
defineProps({
  request: Object,
  id: Number
})
</script>

<style scoped></style>
