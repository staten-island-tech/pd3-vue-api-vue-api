<template>
  <div></div>
</template>

<script>
import { ref, onMounted } from 'vue'
const pokemon = ref('')
async function getPokemon() {
  let result = await fetch(
    'https://data.cityofnewyork.us/resource/erm2-nwe9.json?$$app_token=YetA19ejbBFc3cdnJ207sMngx'
  )
  let data = await result.json()
  pokemon.value = data
}
onMounted(() => {
  getPokemon()
})
</script>
<style lang="scss" scoped></style>
