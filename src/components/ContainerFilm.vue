<template>
  <div>
   

    <header>
      <h1>BOOLFLIX</h1>

      <div id="search">
        <input v-model="inputText" @keyup.enter="searchFilmsSeries(inputText)" type="text">
        <button @click.prevent="searchFilmsSeries(inputText)">Cerca</button>
        <br>
      </div>
    </header>



    <div id="container-film">
      
      <h2>FILM</h2>
      <div class="scroll">
        <div id="film">
          <MyFilm
          id="film"
          v-for="(item, index) in film" :key="index"
          :filmData="item"
          />
        </div>
      </div>
      


      
      <h2>SERIE</h2>
      <div class="scroll">
        <div id="serie">
          <MyFilm
          id="serie"
          v-for="(item, index) in serie" :key="index"
          :filmData="item"
          />
        </div>
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
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #000;
  height: 100px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  h1 {
    color: red;
  }
  
  div#search {
    margin-right: 40px;
  }
}


#container-film{
  height: calc(100vh - 100px);
  background-color: #666;
  margin-top: 100px;
  padding-top: 50px;
  
  h2 {
    font-size: 30px;
    padding: 20px 10px;
  }
    .scroll {
      overflow: auto;
        #film{
          width: 100%;

          display: flex;
          align-items: flex-start;
        
        }

        #serie{
          width: 100%;
          display: flex;
          align-items: center;          
        }
    }
}
</style>