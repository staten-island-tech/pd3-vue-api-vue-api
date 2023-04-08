<template>
  <div class="container">
  <Card></Card>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Card from "../components/Card.vue"
const call = ref('')
async function getCall() {
  let result = await fetch(
    'https://data.cityofnewyork.us/resource/erm2-nwe9.json?$$app_token=YetA19ejbBFc3cdnJ207sMngx'
  )
  let data = await result.json()
  call.value = data
}
onMounted(() => {
  getCall()
})
</script>
<style scoped></style>
