<template>
  <div class="hello">
   

    <input v-model="inputText" @keyup.enter="searchFilms(inputText)" type="text">
    <button @click.prevent="searchFilms(inputText)">Cerca</button>
    <br>



    <MyFilm
      v-for="(item, index) in film" :key="index"
      :filmData="item"
    />
    
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
      apiUrl: "https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&language=it",
      film: [],
      inputText: ""
    }
  },
  created() {
    this.getFilm()
  },
  
  methods: {
    getFilm(){
      if(this.inputText !== "") {

        let currentUrl = this.apiUrl + '&query=' + this.inputText;
        axios
        .get(currentUrl)
        .then((result) => {
            this.film = result.data.results;
            console.log(1 ,this.film);
        })
        .catch(error => {
            console.log("Errore", error);
        })
      }
    },
    searchFilms(userInput){
      this.inputText = userInput;
      console.log(2 , this.inputText);
      this.getFilm();
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
