<template>
  <ul class="m-1">
    <li>Film:</li>
    <li>Titolo: <span>{{movie.title}} </span></li>
    <li>Titolo originale: <span>{{movie.original_title}}</span> </li>
    <li>Lingua originale: <span> {{movie.original_language}} </span></li>
    <li>Media voti: <span>{{movie.vote_average}}</span> </li>  
  </ul>
</template>

<script>
export default {
  name: 'Card',
  props:{
    movie: Object
  }
}
</script>

<style lang="scss" scoped>
ul{
  width: calc(100% / 4);
  min-height: 200px;
  list-style: none;
  background-color: rgb(221, 199, 199);
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