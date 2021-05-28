<template>
  
  <section class="d-flex flex-column align-items-center">
    <h1>{{title[type]}} {{list.length}} </h1>
    
    <div class="d-flex justify-content-evenly flex-wrap">    
      <Card 
        v-for="movie in list"
        :key="movie.id"
        :movie="movie"
      />
    </div>
  </section>
  
</template>

<script>
import Card from './Card.vue';

export default {
  name: 'Main',
  components: {
    Card,
  },
  props:{
    type: String,
    list: Array,
  },
  data(){
    return{
      title:{
        'movie': 'Film trovati:',
        'tv': 'Serie-tv trovate:'
      }
    }
  },
}
</script>

<style lang="scss" scoped>
  section{
    height: calc(100% - 70px);
    div{
      width: 80%;
      margin: 0 auto;
    }
    h1, span{
      font-size: 3rem;
      color: white;
    }
    
  }
</style>