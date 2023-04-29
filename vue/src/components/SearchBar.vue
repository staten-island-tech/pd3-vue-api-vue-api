<template>
  <div>
    <input type="text" v-model="searchTerm" @input="search" placeholder="Search...">
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchTerm: ''
    }
  },
  methods: {
    search() {
      this.$emit('search', this.searchTerm);
    }
  }
}
</script>
