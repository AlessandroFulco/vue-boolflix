<template>
  <div class="hello">
   

   <SearchBar
   @mySearch="inputName"
   />


    <MyFilm
      v-for="(item, index) in film" :key="index"
      :filmData="item"
    />
    
  </div>
</template>

<script>
import axios from 'axios'
import MyFilm from './MyFilm.vue'
import SearchBar from './SearchBar.vue'

export default {
  name: 'ContainerFilm',
  components: {
    MyFilm,
    SearchBar
  },
  data() {
    return {
      apiUrl: "https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=io sono leggenda&language=it",
      film: [],
      inputText: ""
    }
  },
  created() {
    this.getFilm()
  },
  beforeCreate(){
    this.showFilms(this.inputText)
    console.log(this.apiUrl);

  },
  
  methods: {
    getFilm(){
      axios
        .get(this.apiUrl)
        .then(result => {
            this.film = result.data.results;
        })
        .catch(error => {
            console.log("Errore", error);
        })
    },
    inputName(genereUser) {
      this.inputText = genereUser;
      console.log(this.inputText);
      
      
    },
    showFilms(text){
      
      this.apiUrl = "https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=" + text + "&language=it"
    }
  },
  
  
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
