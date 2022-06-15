<template>
    <div>
        <ul>
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
                {{filmData.vote_average}}
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
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
