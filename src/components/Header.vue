<template>
  <header class="d-flex align-items-center justify-content-around">

    <h1>BoolFlix</h1>

    <div class="d-flex align-items-center">
      
      <input 
        v-model.trim="apiQuery"
        type="text"
        placeholder="Cerca film o serie-tv..."
      >

      <button
        class="btn btn-secondary"
        @click="getStartSearch('movie')"
      >
        Cerca Film
      </button>

      <button
        class="btn btn-secondary"
        @click="getStartSearch('tv')"
      >
        Cerca Serie-tv
      </button>

      <button
        class="btn btn-secondary"
        @click=" getStartSearch('all')"
      >
        Cerca Tutto
      </button>

    </div>

  </header>
</template>

<script>


export default {
  name: 'Header',
  components:{
    
  },
  data(){
    return{ 
      apiQuery: ''
    }
  },
  methods:{
    getStartSearch(type){
      this.$emit('startSearch', {text:this.apiQuery, type:type});      
    }
  }

}
</script>

<style lang="scss" scoped>
  header{
    height: 70px;
    background: rgb(0, 0, 0);
    h1{
      text-transform: uppercase;
    }
    input{
      margin-right: 1.5rem;
      padding: 0 1rem;
      outline: none;
    }
    button{
      min-width: 150px;
      text-transform: uppercase;
      margin-left: 0.5rem;
    }
  }
</style>