<template>
    <main class="main bg-dark">
        <!-- ciclo sulla lista dei film -->
        <div class="films-list">
            <h2 v-if="filmsList.length > 0" class="text-white">Film</h2>
            <div class="row row-cols-6 gy-3">
                <div class="col" v-for="(film,i) in filmsList" :key="i">
                    <!-- passo come prop a cardMovie il singolo film su cui sto ciclando -->
                    <CardMovie :info-film="film"></CardMovie>
                </div>
            </div>
        </div>
         
        <div class="series-list pt-5">
            <h2 v-if="seriesList.length > 0" class="text-white">Serie tv</h2>
            <div class="row row-cols-6">
                <div class="col" v-for="(serie,i) in seriesList" :key="i">
                    <!-- passo come prop a cardMovie la singola serie tv su cui sto ciclando -->
                    <CardMovie :info-film="serie"></CardMovie>
                </div>
            </div>
        </div>

    </main>
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
    },
    methods:{
        
    }
    
}
</script>

<style lang="scss" scoped>
.main{
    flex-grow: 1;
    overflow: auto;
    padding: 2rem 1rem
}
</style>