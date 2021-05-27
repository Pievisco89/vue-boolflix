<template>
  <header class="d-flex align-items-center justify-content-around">

    <h1>BoolFlix</h1>

    <div>
      
      <input 
        v-model.trim="apiQuery"
        type="text"
      >

      <button
        @click="$emit('startSearch', {text:apiQuery, type:'movie'})"
      >
        Cerca Film
      </button>

      <button
        @click="$emit('startSearch', {text:apiQuery, type:'tv'})"
      >
        Cerca Serie-tv
      </button>

      <button
        @click="$emit('startSearch', {text:apiQuery, type:'all'})"
      >
        Cerca Tutto
      </button>

      
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
    button{
      text-transform: uppercase;
      margin-left: 0.5rem;
    }
  }
</style>