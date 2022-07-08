<template>
  <div>
    <ais-instant-search :search-client="searchClient" index-name="page">
      <ais-search-box />
      <ais-state-results>
        <template #default="{ results: { hits, query } }">
          <ais-hits v-if="hits.length > 0 && query">
            <div slot="item" slot-scope="{ item }">
              <h2>{{ item.title }}</h2>
              <p>{{ item.content }}</p>
              <p>{{ item._highlightResult }}</p>
            </div>
          </ais-hits>
          <div v-else-if="hits.length === 0 && !query">No results have been found for {{ query }}.</div>
        </template>
      </ais-state-results>
      <!-- <ais-hits>
        <div slot="item" slot-scope="{ item }">
          <h2>{{ item.title }}</h2>
          <p>{{ item.content }}</p>
          <p>{{ item._highlightResult }}</p>
        </div>
      </ais-hits> -->
    </ais-instant-search>
  </div>
</template>

<script>
import { instantMeiliSearch } from '@meilisearch/instant-meilisearch'

export default {
  name: 'IndexPage',
  data() {
    return {
      searchClient: instantMeiliSearch(
        'http://localhost:7700',
        'kyWkTfrc23ad61ad6a6706f1e212a28b2ff47ac21fb95baefb8518ffda6c4e053f2818df'
      ),
    }
  },
  mounted() {
    console.log('SEARCH_API_URL: ' + process.env.SEARCH_API_URL)
    console.log('SEARCH_API_KEY: ' + process.env.SEARCH_API_KEY)
  },
}
</script>
