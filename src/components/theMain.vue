<template>
    <div class="container">
        <!-- ciclo sulla lista dei film -->
        <div v-for="(film,i) in filmsList" :key="i" class="film">
            <!-- passo come prop a cardMovie il singolo film su cui sto ciclando -->
            <CardMovie :info-film="film"></CardMovie>
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
    }
    
}
</script>

<style lang="scss" scoped>

</style>