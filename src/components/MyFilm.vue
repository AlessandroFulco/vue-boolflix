<template>
    <div>

        <ul>
            <li>
                <img :src="'https://image.tmdb.org/t/p/w342' + filmData.poster_path" :alt="filmData.title">
            </li>
            <li>
                {{filmData.title}}{{filmData.name}}
            </li>

            <li>
                {{filmData.original_title}} {{filmData.original_name}}
            </li>

            <li>
                <lang-flag :iso="filmData.original_language" />
            </li>

            <li>
                <!-- {{Math.round(filmData.vote_average / 2)}} -->
                <!-- <font-awesome-icon icon="fa-solid fa-star" v-for="(star, index) in Math.round(filmData.vote_average / 2)" :key="index" /> -->
                <div class="vote">
                    <font-awesome-icon icon="fa-solid fa-star" class="star-white" v-for="(star, index) in voto" :key="index" />
                    <font-awesome-icon icon="fa-regular fa-star" class="star-white" v-for="(star, index) in (5 - voto)" :key="index" />
                    
                </div>
            </li>
        </ul>
        
    </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags';

export default {
  name: 'MyFilm',
  components: {
    LangFlag
  },
  props: {
    filmData : Object
  },
  created(){
    this.log()
  },
  data(){
    return {

        voto: Math.round(this.filmData.vote_average / 2)
    }
  },
  methods: {
    log(){
        console.log(this.voto);
    },
    
  }
  
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    ul {
        list-style-type: none;
        li {
            img {
                width: auto;
                height: 200px;
            }
        }
    }
</style>
