<template>
    <ul>
       <li>{{production.title||production.name}}</li>
       <li>{{production.original_title||production.original_name}}</li>
       <li>
        <img v-if="hasFlag" :src="flagSrc" :alt="production.original_language"/>
       <span v-else>{{production.original_language}}</span> 
        </li>
       <li><img :src="cover" :alt="title"></li>
       
    </ul>
</template>

<script>
const posterUrlRoot = 'https://image.tmdb.org/t/p/w342';
export default{
  name:'ProductionCard',
  
  props:{
    production: Object,
  },
  computed:{
    cover(){
      return  posterUrlRoot + this.production.poster_path;
    },
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