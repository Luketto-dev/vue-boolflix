<template>
    <div class="container">
        <!-- ciclo sulla lista dei film -->
        <div class="films-list">
            <div class="row row-cols-6">
                <div class="col" v-for="(film,i) in filmsList" :key="i">
                    <!-- passo come prop a cardMovie il singolo film su cui sto ciclando -->
                    <CardMovie :info-film="film"></CardMovie>
                </div>
            </div>
        </div>
         
        <div class="series-list pt-5">
            <div class="row row-cols-6">
                <div class="col" v-for="(serie,i) in seriesList" :key="i">
                    <!-- passo come prop a cardMovie la singola serie tv su cui sto ciclando -->
                    <CardMovie :info-film="serie"></CardMovie>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import CardMovie from './CardMovie.vue'

export default {
    components:{
        CardMovie,
    },
    props:{
        // props passata dall app.vue che contiene la lista dei film
        filmsList: Array,
        seriesList: Array,
    }
    
}
</script>

<style lang="scss" scoped>

</style>