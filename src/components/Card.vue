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
            ><span class="me-2">Lingua originale:</span> <CountryFlag country="it" size="normal" /> 
          </li>
          <li 
            v-if="movie.original_language == 'en'" 
            ><span class="me-2">Lingua originale:</span> <CountryFlag country="gb" size="normal" /> 
          </li>
          <li 
            v-if="movie.original_language !== 'en' && movie.original_language !== 'it'" ><span>Lingua originale:</span> {{movie.original_language}} 
          </li>
          <li 
            v-if="movie.overview !== ''"
            class="special"
          > <span>Trama:</span> {{movie.overview}}</li>
          <li 
            v-else
          > <span>Trama:</span> Nessuna descrizione trovata</li>
          <li class="mt-3">
            <span>Voto:</span>
            <div class="stars">
              <div class="empty">
                <div class="inner">
                  <i class="far fa-star"></i>
                  <i class="far fa-star"></i>
                  <i class="far fa-star"></i>
                  <i class="far fa-star"></i>
                  <i class="far fa-star"></i>
                </div>
              </div>
              <div class="solid"
                :style="`width:${8.9*movie.vote_average}px`"
              >
                <div class="inner">
                  <i class="fas fa-star"></i>
                  <i class="fas fa-star"></i>
                  <i class="fas fa-star"></i>
                  <i class="fas fa-star"></i>
                  <i class="fas fa-star"></i>
                </div>
              </div>
            </div>
          </li>

        </ul>

      </div>

    </div>

  </div>
</template>

<script>
import CountryFlag from 'vue-country-flag'; //utilizzo bandierine da country flag

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
    //funzione per il passaggio delle immagini
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
    height: 380px;
    perspective: 1000px;
    margin: 2.5rem;
  }

  .flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;                     
    transition: transform 1.5s;
    transform-style: preserve-3d;
    box-shadow: 0 5px 15px 0 rgba(0, 0, 0, 0.8);
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
    background-color: #9c9797;
    color: black;
    img{
      width: 280px;
      height: 380px;
      border-radius: 20px;
      border: 2px solid rgba(255, 255, 255, 0.39);
    }
  }

  .flip-card-back {
    background-color: rgba(0, 0, 0, 0.9);
    border: 2px solid rgb(255, 255, 255);
    color: white;
    padding: 0.8rem;
    transform: rotateY(180deg);
    text-align: left;
    ul{
      height: 100%;
    }
    li{
      list-style: none;
      width: 100%;
      height: 70px;
      font-size: 1rem;
      & span:first-child{
        font-weight: bold;
        color: rgb(245, 47, 47);
      }
    }
    .special{
      overflow-y: scroll;
      height: 165px;
      span{
        font-weight: bold;
      } 
    }
    .stars{
      position:relative;
      margin-left: 5px;
      .empty, .solid{
        position: absolute;
        top: -25px;
        left: 75px;
        overflow: hidden;
      }
      .inner{
        width: 90px;
      }
    }
  }

  //cambio la misura delle card sotto 1000px
  @media screen and(max-width: 992px){
    .flip-card {
      width: 240px;
      height: 320px;
    }
    .flip-card-front img{
      width: 240px;
      height: 320px;
    }
    .flip-card-back li{
      font-size: 0.85rem;
    }
    .stars{
      margin-top: 5px;
    }
  }
</style>