<template>
<div>
  <SearchBar placeholder="cerca film.." @search="startSearch"/>
  <ResultsSection id="movies" title="movies" :items="movies"/>

  <ResultsSection id="series" title="series" :items="series"/>
</div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import ResultsSection from './components/ResultsSection.vue';
export default {
  name: 'App',
  components:{ SearchBar, ResultsSection,},
  data(){
    return{
      movies:[],
      series:[],
      api:{
        language: 'it-IT',
        key:'e3e416df7064ff3d8ef2cebfaadfaf00',
        baseUri: 'https://api.themoviedb.org/3'
      }
    }
  },
  methods:{
    startSearch(query){
      if(!query){
        this.movies= [];
        this.series = [];
        return;
      }
      const {language, key} = this.api;

      const config = {
        params: {
          api_key: key,
          language,
          query,
        }
      }
      
      this.fetchData('/search/movie',config, 'movies');
      this.fetchData('/search/tv',config, 'series');
    },

    fetchData(endpoint,config, target){
       axios.get(`${this.api.baseUri}${endpoint}`,config).then((res)=>{
          this[target] = res.data.results
       });
    },
  },
};
</script>


<style>

</style>