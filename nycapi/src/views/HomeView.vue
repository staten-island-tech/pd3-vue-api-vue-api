<template>
  <div>
    <SearchBar @search="filterCalls"></SearchBar>
    <div class="container">
      <Card
        v-for="(call, index) in filteredCalls"
        :key="call.unique_key"
        :id="index + 1"
        :request="call"
      >
      </Card>
      <div class="pagination">
        <button v-if="currentPage > 1" @click="currentPage--">Previous</button>
        <button v-if="hasNext" @click="currentPage++">Next</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed, watch } from 'vue'
import Card from '../components/Card.vue'
import SearchBar from '../components/SearchBar.vue'
const calls = ref('')
const filteredCalls = ref('')
let currentPage = ref(1)
const pageSize = 12

async function getCall() {
  let result = await fetch(
    `https://data.cityofnewyork.us/resource/erm2-nwe9.json?$limit=${pageSize}&$offset=${
      (currentPage.value - 1) * pageSize
    }&$$app_token=YetA19ejbBFc3cdnJ207sMngx`
  )
  let data = await result.json()
  calls.value = data
  filteredCalls.value = data
}

watch(currentPage, () => {
  getCall()
})

onMounted(() => {
  getCall()
})

const hasNext = computed(() => {
  return calls.value && calls.value.length === pageSize
})

function filterCalls(searchTerm) {
  filteredCalls.value = calls.value.filter((call) => {
    return (
      (call.incident_address &&
        call.incident_address.toLowerCase().includes(searchTerm.toLowerCase())) ||
      (call.borough && call.borough.toLowerCase().includes(searchTerm.toLowerCase())) ||
      (call.complaint_type &&
        call.complaint_type.toLowerCase().includes(searchTerm.toLowerCase())) ||
      (call.descriptor && call.descriptor.toLowerCase().includes(searchTerm.toLowerCase())) ||
      (call.agency_name && call.agency_name.toLowerCase().includes(searchTerm.toLowerCase())) ||
      (call.agency && call.agency.toLowerCase().includes(searchTerm.toLowerCase())) ||
      (call.incident_zip && call.incident_zip.toLowerCase().includes(searchTerm.toLowerCase())) ||
      (call.closed_date && call.closed_date.toLowerCase().includes(searchTerm.toLowerCase())) ||
      (call.created_date && call.created_date.toLowerCase().includes(searchTerm.toLowerCase())) ||
      (call.status && call.status.toLowerCase().includes(searchTerm.toLowerCase()))
    )
  })
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
  width: 90vw;
  margin: 2rem auto;
}
</style>