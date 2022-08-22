<template>
    <ul>
       <li>{{production.title||production.name}}</li>
       <li>{{production.original_title||production.original_name}}</li>
       <li>
        <img v-if="hasFlag" :src="flagSrc" :alt="production.original_language"/>
       <span v-else>{{production.original_language}}</span> 
        </li>
        <li>
          <FontAwsomeIcon v-for="n in 5" :key="n" :icon="renderStar(n)" />
          {{ vote }}
          </li>
       <li><img :src="cover" :alt="title"></li>
       
    </ul>
</template>

<script>
const posterUrlRoot = 'https://image.tmdb.org/t/p/w342';
const coverPlaceholder = 'https://www.altavod.com/assets/images/poster-placeholder.png';
export default{
  name:'ProductionCard',
  
  props:{
    production: Object,
  },
  computed:{
    vote(){
      return Math.ceil(this.production.vote_average / 2)
    },
    cover(){
      if(!this.production.poster_path) return coverPlaceholder;
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
  methods: {
    renderStar(n){
      const iconType = this.vote >= n ? "fa-solid": "fa-regular";
      return iconType + "fa-star";
    }
  }
}
</script>


<style>

</style>