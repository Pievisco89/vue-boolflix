<template>
  
  <div class="flip-card">
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <img 
          :src="getImg(movie.poster_path)" :alt="movie.title || movie.name" 
        >   
      </div>
      <div class="flip-card-back">
        <ul class="m-1 list-group">
          <li
            v-if="movie.title !== '' || movie.name !== ''"
          ><span>Titolo:</span> <span>{{movie.title || movie.name}}</span> </li>
          <li><span>Titolo originale:</span> <span>{{movie.original_title || movie.original_name}}</span> </li>
          <li 
            v-if="movie.original_language == 'it'" 
            ><span>Lingua originale:</span> <CountryFlag country="it" size="normal" /> 
          </li>
          <li 
            v-if="movie.original_language == 'en'" 
            ><span>Lingua originale:</span> <CountryFlag country="gb" size="normal" /> 
          </li>
          <li 
            v-if="movie.original_language !== 'en' && movie.original_language !== 'it'" >Lingua originale: {{movie.original_language}} 
          </li>
          <li class=" special"
          > <span>Trama:</span> {{movie.overview}}</li>
          <li class="mt-2">
            <i class="fas fa-star"
              v-for="index in Math.round(movie.vote_average/2)"
              :key="index"
            >
            </i>
          </li>     
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import CountryFlag from 'vue-country-flag'

export default {
  name: 'Card',
  data(){
    return{
      baseURL: 'https://image.tmdb.org/t/p/w342/',
  }
  },
  components:{
    CountryFlag
  },
  props:{
    movie: Object
  },
  methods:{
    getImg(img_path){
      let imgURL = this.baseURL+img_path;
      return imgURL;
    }
   
  }
}
</script>

<style lang="scss" scoped>
  .flip-card {
    background-color: transparent;
    width: 280px;
    height: 360px;
    perspective: 1000px;
    margin: 3rem;
  }

  .flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;                     
    transition: transform 1.5s;
    transform-style: preserve-3d;
    box-shadow: 0 5px 10px 0 rgba(0,0,0,0.8);
    border-radius: 18px;

  }

  .flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
  }

  .flip-card-front, .flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    border-radius: 20px;
  }

  .flip-card-front {
    background-color: #bf8484;
    color: black;

    img{
      width:280px;
      height:360px;
      border-radius: 20px;
    }
  }

  .flip-card-back {
    background-color: rgba(0, 0, 0, 0.9);
    color: white;
    padding: 0.8rem;
    transform: rotateY(180deg);
    ul{
      height: 100%;
    }
    li{
      list-style: none;
      width: 100%;
      height: 50px;
      & span:first-child{
        font-weight: bold;
        color: rgb(245, 47, 47);
      }
    }
    .special{
      height: 135px;
      overflow-y: scroll;
      span{
        font-weight: bold;
      } 
    }
  }
</style>