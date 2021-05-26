<template>
  <header class="d-flex align-items-center justify-content-around">

    <h1>BoolFlix</h1>

    <div>
      <input 
        type="text" 
        placeholder="Cerca un film"
        v-model="apiQuery" 
        @keyup.enter="getMovie()" 
      >

      <button
        @click="getMovie()"
      >Cerca</button>

    </div>

  </header>
</template>

<script>
export default {
  name: 'Header',
  data(){
    return{
      apiQuery: ''
    }
  },
  methods:{
    getMovie(){
      this.$emit('searchMovie', this.apiQuery);
      this.apiQuery = '';
    }
  }
}
</script>

<style lang="scss" scoped>
  header{
    height: 70px;
    background: red;
    h1{
      text-transform: uppercase;
    }
    input{
      margin-right: 1.5rem;
      padding: 0 1rem;
      outline: none;
    }
  }
</style>