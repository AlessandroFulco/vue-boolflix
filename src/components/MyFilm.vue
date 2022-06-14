<template>
    <div>
        <ul>
            <li>
                {{filmData.title}}
            </li>

            <li>
                {{filmData.original_title}}
            </li>

            <li>
                {{filmData.original_language}}
            </li>

            <li>
                {{filmData.vote_average}}
            </li>
        </ul>
        
    </div>
</template>

<script>


export default {
  name: 'MyFilm',
  props: {
    filmData : Object
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
