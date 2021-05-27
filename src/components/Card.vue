<template>
  <ul class="m-1 list-group">
    <li class="list-group-item">Titolo: <span>{{movie.title || movie.name}}</span></li>
    <li class="list-group-item">Titolo originale: <span>{{movie.original_title || movie.original_name}}</span> </li>
    <li 
      v-if="movie.original_language == 'it'" 
      class="list-group-item">Lingua originale: <CountryFlag country="it" size="normal" /> 
    </li>
    <li 
      v-if="movie.original_language == 'en'" 
      class="list-group-item">Lingua originale: <CountryFlag country="gb" size="normal" /> 
    </li>
    <li 
      v-if="movie.original_language !== 'en' && movie.original_language !== 'it'" class="list-group-item">Lingua originale: {{movie.original_language}} 
    </li>
    <li class="list-group-item">Media voti: <span>{{movie.vote_average}}</span> </li>  
  </ul>
  
</template>

<script>
import CountryFlag from 'vue-country-flag'

export default {
  name: 'Card',
  data(){
    return{

  }
  },
  components:{
    CountryFlag
  },
  props:{
    movie: Object
  },
  methods:{
   
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