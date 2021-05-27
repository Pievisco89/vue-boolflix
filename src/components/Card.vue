<template>
  <ul class="m-1 list-group">
    <li class="list-group-item">Titolo: <span>{{movie.title || movie.name}}</span></li>
    <li class="list-group-item">Titolo originale: <span>{{movie.original_title || movie.original_name}}</span> </li>
    <li class="list-group-item">Lingua originale: <!-- {{movie.original_language}}   --><CountryFlag :country="getFlag()" size="normal" /> </li>
    <li class="list-group-item">Media voti: <span>{{movie.vote_average}}</span> </li>  
  </ul>
  
</template>

<script>
import CountryFlag from 'vue-country-flag'

export default {
  name: 'Card',
  components:{
    CountryFlag
  },
  props:{
    movie: Object
  },
  methods:{
    getFlag(){
      if(this.movie.original_language === 'it'){
        return 'it'
      } else if (this.movie.original_language === 'en'){
        return 'gb'
      }
        return this.movie.original_language
    }
  }
}
</script>

<style lang="scss" scoped>
ul{
  width: calc(100% / 4);
  min-height: 200px;
  list-style: none;
  border-radius: 2rem;
  padding-top: 1rem;
  li{
    text-transform: capitalize;
    font-size: 1rem;
    span{
      text-decoration: underline;
      color: red;
    }
  }
}
</style>