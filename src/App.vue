<template>
  <div id="app">
    
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: 'App',
  components: {
    
  },
  methods:{
    fetchFilmsList(){
      axios.get("https://api.themoviedb.org/3/search/movie",{
        params:{
          api_key:"943dadb8ae5a51623bdae45efd2fc1ad"
        }
      })
    }
  }
}
</script>

<style lang="scss">
@import "./assets/scss/main.scss";

</style>
