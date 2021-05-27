<template>
  <ul class="m-1 list-group">
    <li class="list-group-item">Titolo: <span>{{movie.title || movie.name}}</span></li>
    <li class="list-group-item">Titolo originale: <span>{{movie.original_title || movie.original_name}}</span> </li>
    <li class="list-group-item">Lingua originale: <span> {{movie.original_language}} </span></li>
    <li class="list-group-item">Media voti: <span>{{movie.vote_average}}</span> </li>  
  </ul>
  
</template>

<script>
export default {
  name: 'Card',
  props:{
    movie: Object
  },
  data(){
    return{
      
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