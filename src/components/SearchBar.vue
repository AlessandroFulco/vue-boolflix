<template>
    <div>
        
        <input type="text" v-model="inputName" @keyup.enter="searchFilm()">
        
        <button  @click="searchFilm()">Cerca</button>
        
    </div>
</template>

<script>



export default {
    name: 'SearchBar',

    data(){
        return {
            inputName : "",
        }
    },

    methods: { 
        searchFilm() {
            this.$emit('mySearch', this.inputName);
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
