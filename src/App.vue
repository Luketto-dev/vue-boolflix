<template>
  <div id="app">
      <!-- ascolto l evento passato da TheHeader.vue -->
      <TheHeader @searchFilms="onSearchFilms" :genres-films="genresFilms" :genres-series="genresSeries"></TheHeader>

      <!-- passo la prop che contiene la lista dei film a TheMain.vue -->
      <TheMain :films-list="filmsList" :series-list="seriesList"></TheMain>
    
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
      seriesList : [],
      searchFilms: "",
      
      genresFilms: [],
      genresSeries: [],

    }
  },
  methods:{
    // chiamata api, l argomento lo prendiamo dall emit che ci ha passato TheHeader.vue 
    fetchFilmsList(type){
      if (!this.searchFilms) {
        return
      }
      axios.get("https://api.themoviedb.org/3/search/" + type,{
        params:{
          api_key:"943dadb8ae5a51623bdae45efd2fc1ad",
          query: this.searchFilms,
          language: "it-IT"
        }
      }).then(resp => {
        // salvo la risposta dell api all interno di un data che ho chiamato filmsList
        if (type === "movie") {
          this.filmsList = resp.data.results
        }
        else{
          this.seriesList = resp.data.results
        }
        
      })
    },
    fetchGenresFilms(type){
      axios.get("https://api.themoviedb.org/3/genre/" + type + "/list",{
        params:{
          api_key:"943dadb8ae5a51623bdae45efd2fc1ad",
          language: "it-IT"
        }
      }).then(resp => {
        // salvo la risposta dell api all interno di un data che ho chiamato filmsList
        if (type === "movie") {
          this.genresFilms = resp.data.genres
        }
        else{
          this.genresSeries = resp.data.genres
        }
        
      })
    },
    
    // quando faccio la ricerca del film salvo in un data il dato che ci ha passato TheHeader.vue e invoco la chiamata api passando per argomento il dato appena salvato
    onSearchFilms(searchFilms){
      
      this.searchFilms = searchFilms
      this.fetchFilmsList("movie")
      this.fetchFilmsList("tv")

    },
    
  },
  
  mounted(){
    this.fetchGenresFilms("movie")
  }
}
</script>

<style lang="scss">
@import "./assets/scss/main.scss";

</style>
