<template>
    <ul>
       <li>{{production.title||production.name}}</li>
       <li>{{production.original_title||production.original_name}}</li>
       <li>
        <img v-if="hasFlag" :src="flagSrc" :alt="production.original_language"/>
       <span v-else>{{production.original_language}}</span> 
        </li>
       <li>{{production.vote_average}}</li>
    </ul>
</template>

<script>
export default{
  name:'ProductionCard',
  props:{
    production: Object,
  },
  computed:{
    hasFlag(){
      const flag =['it','en'];
      return flag.includes(this.production.original_language);
    },
    flagSrc(){
        return require(`../assets/img/flags/${this.production.original_language}.png`)
    },
  },
}
</script>


<style>

</style>