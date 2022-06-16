<template>
    <div>
        <section>
            <img :src="'https://image.tmdb.org/t/p/w342' + filmData.poster_path" :alt="filmData.title">
            <ul>
                <li>
                    <span>Titolo: </span> {{filmData.title}}{{filmData.name}}
                </li>

                <li>
                    <span>Titolo originale: </span> {{filmData.original_title}} {{filmData.original_name}}
                </li>
                <li>
                    <div class="vote">
                        Voto: 
                        <font-awesome-icon icon="fa-solid fa-star" class="star_color" v-for="(star, index) in voto" :key="index" />
                        <font-awesome-icon icon="fa-regular fa-star" class="star_color" v-for="(star, j) in (5 - voto)" :key="j + 'i'" />
                    </div>
                </li>
                <li>
                    <span>Overview: </span> {{filmData.overview}}
                </li>
                <!-- <li>
                    <lang-flag :iso="filmData.original_language" />
                </li> -->

            </ul>
        </section>
    </div>
</template>

<script>
// import LangFlag from 'vue-lang-code-flags';

export default {
  name: 'MyFilm',
  components: {
    // LangFlag
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
    } 
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    div {
        width: 100%;
        section {
            width: 100%;
            position: relative;
            &:hover {
                ul {
                    display: block;
                    position: absolute;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    background-color: #000;
                    color: #fff;
                    padding: 10px;
                    list-style-type: none;
                    li {
                        
                        padding: 2px;
                        span {
                            font-weight: bold;
                        }
                        .star_color {
                            color: yellow;
                        }
                    }
                }
            }
        }
        ul {
            display: none;
        }

        
    }
</style>
