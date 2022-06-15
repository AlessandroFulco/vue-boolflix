<template>
  <div class="hello">
   

    <input v-model="inputText" @keyup.enter="searchFilmsSeries(inputText)" type="text">
    <button @click.prevent="searchFilmsSeries(inputText)">Cerca</button>
    <br>



    <div id="container-film">
      <div id="film">
        <h1>film</h1>
        <MyFilm
          v-for="(item, index) in film" :key="index"
          :filmData="item"
        />
      </div>


      <div id="serie">
        <h1>Serie</h1>
        <MyFilm
          v-for="(item, index) in serie" :key="index"
          :filmData="item"
        />
      </div>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'
import MyFilm from './MyFilm.vue'


export default {
  name: 'ContainerFilm',
  components: {
    MyFilm,
  },
  data() {
    return {
      apiUrlFilm: "https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&language=it&include_adult=true",
      apiUrlSeriesTv: "https://api.themoviedb.org/3/search/tv?api_key=9f8a6b1b64c92ae4e9fd6923fcb6d8a3&language=it&include_adult=true",
      film: [],
      serie: [],
      inputText: "",
    }
  },
  created() {
    this.getFilm();
    this.getSeriesTV();
  },
  
  methods: {
    // chiamata Api per i film
    getFilm(){
      if(this.inputText !== "") {

        let currentUrl = this.apiUrlFilm + '&query=' + this.inputText;
        axios
        .get(currentUrl)
        .then((result) => {
            this.film = result.data.results;
            console.log("film", this.film);
        })
        .catch(error => {
            console.log("Errore", error);
        })
      }
      
      
    },
    // chiamata Api serie tv
    getSeriesTV(){
      if(this.inputText !== "") {

        let currentUrl = this.apiUrlSeriesTv + '&query=' + this.inputText;
        axios
        .get(currentUrl)
        .then((result) => {
            this.serie = result.data.results;
            console.log("serie", this.serie);
        })
        .catch(error => {
            console.log("Errore", error);
        })
      }
    },

    searchFilmsSeries(userInput){
      this.inputText = userInput;
      this.getFilm();
      this.getSeriesTV();
    }


  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#container-film{
  display: flex;
  justify-content: center;
  gap: 300px;
}
</style>