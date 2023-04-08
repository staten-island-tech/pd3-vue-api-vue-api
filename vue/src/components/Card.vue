<template>
  <div class="card">
    <h2>{{ complaintType }}</h2>
    <p>{{ description }}</p>
    <p>Called {{ agencyName }}</p>
    <p>Address:{{ address }}</p>
    <p>Date:{{ date }}</p>
    <p>{{ borough }}</p>
  </div>
</template>

<script setup>
defineProps({
  borough: String,
  status: String,
  date: String, //create method for date
  address: String,
  agencyName: String,
  complaintType: String,
  description: String
})
</script>

<style scoped></style>
