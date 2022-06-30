<template>
    <div class="movie h-100 position-relative" >
        <div class="poster-img h-100">
            <img class="w-100 h-100" :src="urlPoster" alt="">
        </div>

        <div class="movie-overlay">
        
            <div class="movie-title">
                <h5>Titolo film: {{movieTitle}}</h5>
            </div>
            <div class="original-title">
                Titolo originale: {{movieOriginalTitle}}
            </div>
            <div class="language" >
                Lingua: <span class="fi" :class="'fi-' + countryFlag"></span>
            </div>
            <span>Voto: </span>
            <span class="vote" v-for="i in 5" :key="i">
                <i v-if="i <= voteUpdate(infoFilm.vote_average)" class="fa-solid fa-star text-warning"></i>
                <i v-else class="fa-regular fa-star"></i>
            </span>
            <div class="description">
                Descrizione: 
                <span v-if="infoFilm.overview">{{infoFilm.overview}}</span>
                <span v-else>Descrizione non disponibile</span>
            </div>

        </div>
        
    </div>
    
</template>

<script>

export default {
    data(){
        return{
            detailsGenres: [], 
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
                "ko" : "kr"
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
            return Math.round(vote/2)
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