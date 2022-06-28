<template>
    
        <ul class="info-film border border-dark">
            <li>Titolo film: {{infoFilm.title}}</li>
            <li>Titolo originale: {{infoFilm.original_title}}</li>
            <li>Lingua: {{infoFilm.original_language}}</li>
            <li>voto: {{infoFilm.vote_average}}</li>
        </ul>
    
</template>

<script>
export default {
    props:{
        // prop inviata da themain.vue che contiene le informazioni di ogni singolo film
        infoFilm: Object
    }
}
</script>

<style lang="scss" scoped>

</style>