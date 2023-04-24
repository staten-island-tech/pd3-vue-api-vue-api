<template>
<<<<<<< Updated upstream
  <div class="container">borough="call.borough"
    <Card v-for="(call, index) in calls" :key="call.unique_key" :id="index + 1" :request="call"> </Card>
=======
  <div class="container">
    <Card v-for="(call, index) in calls" :key="call.unique_key" :id="index + 1" :request="call"> </Card>
    <div class="pagination">
      <button v-if="currentPage > 1" @click="currentPage--">Previous</button>
      <button v-if="hasNext" @click="currentPage++">Next</button>
    </div>
>>>>>>> Stashed changes
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Card from '../components/Card.vue'
const calls = ref('')
<<<<<<< Updated upstream
=======
let currentPage = ref(1)
const pageSize = 12

>>>>>>> Stashed changes
async function getCall() {
  let result = await fetch(
    'https://data.cityofnewyork.us/resource/erm2-nwe9.json?$$app_token=YetA19ejbBFc3cdnJ207sMngx'
  )
  let data = await result.json()
  calls.value = data
}
onMounted(() => {
  getCall()
})
<<<<<<< Updated upstream
=======

const hasNext = computed(() => {
  return calls.value && calls.value.length === pageSize
})
>>>>>>> Stashed changes
</script>
<style scoped></style>
