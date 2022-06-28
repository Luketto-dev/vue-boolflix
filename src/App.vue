<template>
  <div id="app">
      <!-- scolto l evento passato da TheHeader.vue -->
      <TheHeader @searchFilms="onSearchFilms"></TheHeader>

      <!-- passo la prop che contiene la lista dei film a TheMain.vue -->
      <TheMain :films-list="filmsList"></TheMain>
    
  </div>
</template>

<script>
import TheHeader from "./components/theHeader.vue"
import TheMain from "./components/theMain.vue"
import axios from "axios"

export default {
  name: 'App',
  components: {
    TheHeader,
    TheMain,
  },
  data(){
    return{
      filmsList : [],
      searchFilms: ""
    }
  },
  methods:{
    // chiamata api, l argomento lo prendiamo dall emit che ci ha passato TheHeader.vue 
    fetchFilmsList(searchFilms){
      axios.get("https://api.themoviedb.org/3/search/movie",{
        params:{
          api_key:"943dadb8ae5a51623bdae45efd2fc1ad",
          query: searchFilms,
          language: "it-IT"
        }
      }).then(resp => {
        // salvo la risposta dell api all interno di un data che ho chiamato filmsList
        this.filmsList = resp.data.results
      })
    },
    // quando faccio la ricerca del film salvo in un data il dato che ci ha passato TheHeader.vue e invoco la chiamata api passando per argomento il dato appena salvato
    onSearchFilms(searchFilms){
      
      this.searchFilms = searchFilms
      this.fetchFilmsList(this.searchFilms)
    }
  },
  
  mounted(){
    
  }
}
</script>

<style lang="scss">
@import "./assets/scss/main.scss";

</style>
