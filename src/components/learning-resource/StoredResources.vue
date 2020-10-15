<template>
  <ul>
    <learning-resouce
      v-for="res in resources"
      :key="res.id"
      :id= "res.id"
      :title="res.title"
      :description="res.description"
      :link="res.link"
    ></learning-resouce>
  </ul>
</template>

<script>
import LearningResouce from './LearningResource.vue';
export default {
    components: {
        LearningResouce
    },
    inject: ["resources"] //provided in the TheResource
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>