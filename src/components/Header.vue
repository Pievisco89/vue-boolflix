<template>
  <header class="d-flex align-items-center">

    <div class="d-flex justify-content-evenly align-items-center">
      <h1>BoolFlix</h1>
      
      <input 
        class="form-control"
        v-model.trim="apiQuery"
        type="text"
        placeholder="Cerca film o serie-tv..."
      >

      <button
        class="btn btn-secondary btn-sm small"
        @click="getStartSearch('movie')"
      >
        Film
      </button>

      <button
        class="btn btn-secondary btn-sm ms-1 small"
        @click="getStartSearch('tv')"
      >
        Serie-tv
      </button>

      <button
        class="btn btn-secondary btn-sm ms-1 small"
        @click=" getStartSearch('all')"
      >
        Cerca Tutto
      </button>

      <button
        class="btn btn-secondary btn-sm ms-1"
        @click=" getStartSearch('all')"
      >
        Cerca
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
    div{
      width: 90%;
      margin: 0 auto;
      h1{
        text-transform: uppercase;
      }
      input{
        margin: 0 1.25rem;
        padding: 0 1rem;
        outline: none;
        &::placeholder {
          font-size: 0.85rem;
        }
      }
      button{
        min-width: 100px;
        font-size: 0.75rem;
        text-transform: uppercase;
        
      }
    }

  }
  
  //gestisco input e display bottoni sotto 800px
  @media screen and(max-width: 800px){
    div{
      width: 100%;
      h1{
        font-size: 1.45rem;
      }
      input{
        min-width: 150px;
      }
      .small{
        display: none;
      } 
      & button:last-child{
        display: visible;
      }    
    }
  }
  
  @media screen and(min-width: 801px){
    div button:last-child{
    display: none;
    }
  }
</style>