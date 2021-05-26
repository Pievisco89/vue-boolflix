<template>
  <div id="app">
    <Header 
      @searchMovie="this.searchingMovie"
    />
    
    <Main 
      v-if="loading === false"
      :movieList="movieList"
    />

    <Default 
      v-else
    />
  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header.vue'
import Main from './components/Main.vue'
import Default from './components/Default.vue'



export default {
  name: 'App',
  components: {
    Header,
    Main,
    Default
  },
  data(){
    return{
      loading: true,
      movieList: [],
      apiURL: 'https://api.themoviedb.org/3/search/movie',
      apiKey: 'fd1b976883e42bd0bfd6acabdc7587a9',
      apiQuery: ''
    }
  },
  methods:{
    searchingMovie(text){
      this.apiQuery = text;
      this.getData();
      if(this.apiQuery === ''){
        this.loading = true;
      }
    },
    getData(){
      axios.get(this.apiURL,{
        params:{
          api_key: this.apiKey,
          query: this.apiQuery,
          language: 'it-IT'
        }
      })
      .then(resp =>{
        this.movieList = resp.data.results;
        this.loading = false;
      })
      .catch(err => {
        console.log(err);
      })
    }
    
  }
}
</script>

<style lang="scss">
  @import './assets/style/general.scss';

</style>
