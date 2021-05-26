<template>
  <div id="app">
    <span>ciao</span>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      apiURL: 'https://api.themoviedb.org/3/search/movie',
      apiKey: 'fd1b976883e42bd0bfd6acabdc7587a9',
      query: 'ritorno al futuro'
    }
  },
  created(){
    axios.get(this.apiURL,{
      params:{
        api_key: this.apiKey,
        query: this.query,
        language: 'it-IT'
      }
    })
    .then(resp =>{
      console.log(resp.data);
    })
    .catch(err => {
      console.log(err);
    })
    
  }
}
</script>

<style lang="scss">

</style>
