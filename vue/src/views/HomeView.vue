<template>
  <div>
    <div class="container">
      <Card
        v-for="(call, index) in calls"
        :key="call.unique_key"
        :id="index + 1"
        :request="call"
      >
      </Card>
      </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Card from '../components/Card.vue'
const calls = ref('')

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