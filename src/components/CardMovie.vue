<template>
    <div class="movie border border-dark h-100">
        <div class="movie-title">
            <h5>Titolo film: {{movieTitle}}</h5>
        </div>
        <div class="original-title">
            Titolo originale: {{movieOriginalTitle}}
        </div>
        <div class="language">
            Lingua: {{infoFilm.original_language}}
        </div>
        <div class="vote">
            voto: {{infoFilm.vote_average}}
        </div>
    </div>
    
</template>

<script>
export default {
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
    }
}
</script>

<style lang="scss" scoped>

</style>