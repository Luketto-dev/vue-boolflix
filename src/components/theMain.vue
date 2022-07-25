<template>
    <main class="main bg-dark">
        <!-- ciclo sulla lista dei film -->
        <transition
        enter-active-class="animate__animated animate__fadeInRightBig"
        leave-active-class="animate__animated animate__fadeOutLeftBig"
        >
        <div v-if="showFilmsList && filmsList != ''" class="films-list">
        
            <h2 class="text-white">Film</h2>
            <div class="row row-cols-6 gy-3">
                <div class="col" v-for="(film,i) in filmsList" :key="i">
                    <!-- passo come prop a cardMovie il singolo film su cui sto ciclando -->
                    
                    <CardMovie :info-film="film"></CardMovie>
                    
                </div>
            </div>
        </div>
        </transition>
        
        <transition
        enter-active-class="animate__animated animate__fadeInRightBig"
        leave-active-class="animate__animated animate__fadeOutLeftBig"
        >
        <div v-if="showFilmsList && filmsList != ''" class="series-list pt-5">
            <h2 class="text-white">Serie tv</h2>
            <div class="row row-cols-6 gy-3">
                <div class="col" v-for="(serie,i) in seriesList" :key="i" >
                    <!-- passo come prop a cardMovie la singola serie tv su cui sto ciclando -->
                    
                    <CardMovie :info-film="serie"></CardMovie>
                    
                </div>
            </div>
        </div>
        </transition>

        <transition
        leave-active-class="animate__animated animate__fadeOutDownBig"
        >
            <div v-if="filmsList.length === 0" class="intro-page text-center text-italic">
                <h2 >Benvenuto in</h2>
                <img class="w-50" src="../../public/logo.png" alt="">
                <h2>Cerca il titolo del film che ti interessa tra milioni di film per avere informazioni e dattagli</h2>
            </div>
        </transition>

    </main>
</template>

<script>

import CardMovie from './CardMovie.vue'

export default {
    data(){
        return{
            
        }
    },
    components:{
        CardMovie,
    },
    props:{
        // props passata dall app.vue che contiene la lista dei film
        filmsList: Array,
        seriesList: Array,
        showFilmsList: Boolean
        
    },/*
    methods:{
        closeIntro(){
            this.showIntro = false;
        }
    },
    mounted(){
        setTimeout(this.closeIntro, 3000)
    }*/
}
</script>

<style lang="scss" scoped>

.main{
    flex-grow: 1;
    overflow: auto;
    padding: 2rem 1rem;

    & .intro-page{
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        color:#757575
        
    }

}
</style>