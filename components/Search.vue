<!-- <template>
    <div>
      <h1>
        [Client] Algolia Search Results for query: 'Samsung' with optional filters
      </h1>
      {{ result }}
      <h2>[SSR] Algolia Search Result for query: 'Samsung'</h2>
      {{ data }}
    </div>
  </template>
  
  <script setup>
  const { result, search } = useAlgoliaSearch('test_index'); // pass your index as param
  onMounted(async () => {
    await search({
      query: 'Samsung',
      requestOptions: { filters: 'objectID:ecommerce-sample-data-99' },
    });
  });
  
  const { data } = await useAsyncAlgoliaSearch({
    indexName: 'wser',
    query: 'Samsung',
  });
  </script> -->

<script lang="ts" setup>
    import { AisInstantSearch, AisSearchBox, AisHits } from 'vue-instantsearch/vue3/es'
    const indexName = 'wser' 
    const algolia = useAlgoliaRef()
</script>

<template>
    <div>
      <ais-instant-search :index-name="indexName" :search-client="algolia">
        <ais-search-box />
        <ais-hits />
      </ais-instant-search>
    </div>
  </template>
  