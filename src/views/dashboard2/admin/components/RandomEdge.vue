<template>
  <div v-if="edges.results.length > 0 && edges.results[currentIndex]" class="card">
    <div class="card-img">
      <transition :name="imgTransition">
        <img
          :key="edges.results[currentIndex].edge_id"
          :src="edges.results[currentIndex].edge_img.large"
          alt="Edge Image"
        >
      </transition>
    </div>
    <ul>
      <li>ID: {{ edges.results[currentIndex].edge_id }}</li>
      <li>{{ edges.results[currentIndex].edge_name }}</li>
      <li>{{ edges.results[currentIndex].edge_version }}</li>
      <li>{{ edges.results[currentIndex].edge_config }}</li>
    </ul>
  </div>
</template>

<script>
import { reactive } from 'vue'

export default {
  setup() {
    const edges = reactive({ results: [] });
    (async() => {
      try {
        const res = await fetch('http://163.18.44.158:9000/edge_view/?format=api')
        const resJSON = await res.json()
        edges.results = resJSON.results
      } catch (err) {
        console.log(err)
      }
    })()
    return {
      edges
    }
  }
}
</script>

<style scoped lang="scss">

</style>
