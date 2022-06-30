<template>
    <div class="movie h-100 position-relative" 
        @mouseenter="fetchGenresFilm(infoFilm.title ? 'movie' : 'tv'), fetchactorsfilm(infoFilm.title ? 'movie' : 'tv')">
        <div class="poster-img h-100">
            <img class="w-100 h-100" :src="urlPoster" alt="">
        </div>

        <div class="movie-overlay">
        
            <div class="movie-title">
                <h5 class="fw-bold">Titolo film: {{movieTitle}}</h5>
            </div>
            <div class="original-title">
                <span class="fw-bold">Titolo originale: </span>  
                <span>{{movieOriginalTitle}}</span> 
            </div>
            <div class="language" >
                <span class="fw-bold">Lingua: </span> 
                <span class="fi" :class="'fi-' + countryFlag"></span>
            </div>
            <div class="vote">
                <span class="fw-bold">Voto: </span>
                <span v-for="i in 5" :key="i">
                    <i v-if="i <= voteUpdate(infoFilm.vote_average)" class="fa-solid fa-star text-warning"></i>
                    <i v-else class="fa-regular fa-star"></i>
                </span>
            </div>
            <div class="genres" >
                <span class="fw-bold">Genere: </span>  
                <span v-for="(genre, i) in detailsGenres" :key="i">{{genre.name}}, </span>
            </div>
            <div class="cast">
                <span class="fw-bold">Cast: </span>
                <span v-for="(actor, i) in castFilm" :key="i">{{actor.name}}, </span>
            </div>
            <div class="description">
                <span class="fw-bold">Descrizione: </span>
                <span v-if="infoFilm.overview">{{infoFilm.overview}}</span>
                <span v-else>Descrizione non disponibile</span>
            </div>

        </div>
        
    </div>
    
</template>

<script>
import axios from "axios"

export default {
    data(){
        return{
            detailsGenres: [],
            castFilm : []
        }
    },
    props:{
        // prop inviata da themain.vue che contiene le informazioni di ogni singolo film
        infoFilm: Object,
        
    },
    computed: {
        movieTitle(){
            if (this.infoFilm.title) {
                return this.infoFilm.title
            }
            return this.infoFilm.name
        },
        movieOriginalTitle(){
            if (this.infoFilm.original_title) {
                return this.infoFilm.original_title
            }
            return this.infoFilm.original_name
        },
        countryFlag(){
            const langsMaps = {
                "en" : "us",
                "ja" : "jp",
                "zh" : "cn",
                "ko" : "kr",
                "el" : "gr"
            }
            if (langsMaps[this.infoFilm.original_language]) {
                return langsMaps[this.infoFilm.original_language]
            }

            return this.infoFilm.original_language
        },
        urlPoster(){
            if (this.infoFilm.poster_path) {
                return "https://image.tmdb.org/t/p/w342/" + this.infoFilm.poster_path
            }
            
            return "/imgError.png"
        },
        

    },
    methods:{
        voteUpdate(vote){
            return Math.ceil(vote/2)
        },

        fetchGenresFilm(type){
            axios.get("https://api.themoviedb.org/3/" + type + "/" + this.infoFilm.id,{
            params:{
                api_key:"943dadb8ae5a51623bdae45efd2fc1ad",
                language: "it-IT"
            }
        }).then(resp => {
            this.detailsGenres = resp.data.genres           
        })

        },

        fetchactorsfilm(type){
            axios.get("https://api.themoviedb.org/3/" + type + "/" + this.infoFilm.id + "/credits",{
            params:{
                api_key:"943dadb8ae5a51623bdae45efd2fc1ad",
                language: "it-IT"
            }
        }).then(resp => {
            this.castFilm = resp.data.cast.slice(0,5)
            
        })
        },

    },
    mounted(){
        
    }
}
</script>

<style lang="scss" scoped>
.movie{
    & .movie-overlay{
        position: absolute;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        background-color: black;
        opacity: 0;
        color: white;
        padding: 1rem;
        transition: opacity .4s ease-in-out;
        overflow: auto;

        &:hover{
            opacity: 0.8
        }

        
    }
}
</style>