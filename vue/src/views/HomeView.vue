<template>
  <div>
    <div>311 Calls from 2010 to the present</div>
    <div class="container">
      <Card
        v-for="(call, index) in calls"
        :key="call.unique_key"
        :id="index + 1"
        :request="call"
      >
      </Card>
    </div>
    <div class="pagination">
      <button v-if="currentPage > 1" @click="prevPage()">Previous</button>
      <span>Page {{ currentPage }}</span>
      <button v-if="calls.length === pageSize" @click="nextPage()">Next</button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Card from '../components/Card.vue'
const calls = ref('')
const currentPage = ref(1)
const pageSize = 12

async function getCall() {
  let offset = (currentPage.value - 1) * pageSize
  let result = await fetch(
    `https://data.cityofnewyork.us/resource/erm2-nwe9.json?$limit=${pageSize}&$offset=${offset}&$order=created_date DESC&$$app_token=YetA19ejbBFc3cdnJ207sMngx`
  )
  let data = await result.json()
  calls.value = data
}

function nextPage() {
  currentPage.value ++ 
  getCall()
}

function prevPage() {
  currentPage.value --
  getCall()
}

onMounted(() => {
  getCall()
})
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