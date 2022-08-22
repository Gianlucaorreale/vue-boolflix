<template>
  <section :id="id">
    <h2 v-if="title">{{ title }}</h2>
    <ProductionCard v-for="item in items" 
    :key="item.id" 
    :production="item"/>
  </section>
</template>

<script>
  import ProductionCard from './ProductionCard.vue'
  export default {
    name: 'ResultsSection',
    components:{ProductionCard},
    props:{
        id: {type: String, required: false},
        title: {type: String, required: false},
        items: {type: Array, required: true}
    }
  }
</script>

<style>

</style>