<template>
  <div id="app">
    


    <ContainerFilm/>
    


  </div>
</template>

<script>
import ContainerFilm from './components/ContainerFilm.vue'


export default {
name: 'App',
  components: {
    ContainerFilm
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Helvetica, Arial, sans-serif;
  
}
</style>
