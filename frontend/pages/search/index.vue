<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <h1>hello world</h1>
    <input class="border-2" v-model="query" type="text" @change="search" />

    <div>
      <div v-for="hit in results" :key='`search-hit-${hit.id}`'>
        {{ hit }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: '',
      results: [],
    }
  },
  methods: {
    search() {
      this.results = []
      this.$axios.setHeader(
      'Authorization',
      'Bearer ' + process.env.SEARCH_API_KEY
    )
      this.$axios
        .$get('http://localhost:7700/indexes/page/search?q=' + this.query)
        .then((res) => {
          // add res.hits to results
          this.results = this.results.concat(res.hits)
        })
      this.$axios
        .$get('http://localhost:7700/indexes/publication/search?q=' + this.query)
        .then((res) => {
          // add res.hits to results
          this.results = this.results.concat(res.hits)
        })


    },
  },
}
</script>

<style>
</style>