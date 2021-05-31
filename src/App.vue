<template>
  <div id="app" class="text-center">
    <!-- richiamo la funzione startSearch al click sui bottoni -->
    <Header 
      @startSearch="startSearch"
    />

    <!-- da visualizzare in assenza di risultati -->
    <h1
      class="m-5"
      v-if="resultList.movie.length === 0 && resultList.tv.length === 0"
    >Nessun risultato trovato</h1>


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

  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header.vue';
import Main from './components/Main.vue';


export default {
  name: 'App',
  components: {
    Header,
    Main,

  },
  data(){
    return{    
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
    //in base al bottone cliccato partono chiamate API
    startSearch(obj){
      this.resetList();
      if(obj.type === 'all'){
        this.callAPI(obj.text, 'movie');
        this.callAPI(obj.text, 'tv');
      }else{
        this.callAPI(obj.text, obj.type)
      }
    },

    //funzione per resettare i due array prima di fare una nuova chiamata
    resetList(){
      this.resultList.movie = [],
      this.resultList.tv = []
    },

    //chiamata Api che avviene al momento del click sul bottone
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
        })
        .catch(err => {
          console.log(err);
        })

      }
    },

  },
  //creo una visualizzazione di base con film e serie più popolari
  created(){ 
    let type = 'movie'
    axios.get('https://api.themoviedb.org/3/movie/popular',{
      params:{
        api_key: this.apiKey,
        language: 'it-IT'
      }
    })
    .then(resp => {
      this.resultList[type] = resp.data.results;       
    })
    .catch(err => {
      console.log(err);
    })

    let typeTv = 'tv'
    axios.get('https://api.themoviedb.org/3/tv/popular',{
      params:{
        api_key: this.apiKey,
        language: 'it-IT'
      }
    })
    .then(resp => {
      this.resultList[typeTv] = resp.data.results;       
    })
    .catch(err => {
      console.log(err);
    })
  }
  
  
}
</script>

<style lang="scss">
  @import './assets/style/general.scss';
  
  h1{
    color: rgb(255, 0, 0);
  }

</style>
