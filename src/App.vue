<template>
  <div id="app">
    <Header 
      @startSearch="startSearch"
    />

    <h1
      v-if="resultList.movie.length === 0 && resultList.movie.length === 0"
    >Nessun risultato trovato</h1> <!-- da sistemare -->

    <Main
      v-if="resultList.movie.length > 0"
      type="movie"
      :list="resultList.movie"
    />

    <Main
      v-if="resultList.tv.length > 0"
      type="tv"
      :list="resultList.tv"
    />

    <!-- <Default 
      v-else
    /> -->


  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header.vue';
import Main from './components/Main.vue';
//import Default from './components/Default.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main,
    /* Default */
  },
  data(){
    return{
      loading: true,    
      apiURL: 'https://api.themoviedb.org/3/search/',
      apiKey: 'fd1b976883e42bd0bfd6acabdc7587a9',
      apiQuery: '',
      resultList: {
        'movie': [],
        'tv': [],
      },
    }
  },
  methods:{

    startSearch(obj){
      this.resetList();
      if(obj.type === 'all'){
        this.callAPI(obj.text, 'movie');
        this.callAPI(obj.text, 'tv');
      }else{
        this.callAPI(obj.text, obj.type)
      }
    },

    resetList(){
      this.resultList.movie = [],
      this.resultList.tv = []
    },

    callAPI(query, type){
      if(query !== ''){
        axios.get(this.apiURL+type,{
          params:{
            api_key: this.apiKey,
            query: query,
            language: 'it-IT'
          }
        })
        .then(resp => {
          this.resultList[type] = resp.data.results;
          console.log(this.resultList);
        })
        .catch(err => {
          console.log(err);
        })

      }
    },

  },
  
  
}
</script>

<style lang="scss">
  @import './assets/style/general.scss';

</style>
