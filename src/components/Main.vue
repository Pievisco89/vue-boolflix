<template>
  
  <section class="d-flex">
    <div class="d-flex justify-content-center flex-wrap">
      <Card 
        :movie="movie"
        v-for="(movie, index) in movieList"
        :key="index"
      />
    </div>
  </section>
</template>

<script>
import Card from './Card.vue';

export default {
  name: 'Main',
  props:{
    movieList: Array
  },
  components: {
    Card,
  }
}
</script>

<style lang="scss" scoped>
  section{
    height: calc(100% - 70px);
    div{
      width: 80%;
      margin: 0 auto;
    }
    
  }
</style>