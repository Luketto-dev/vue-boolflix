<template>
    <header class="py-2 px-5 bg-dark">
        <div class="my-nav d-flex">
            <div class="nav-logo">
                <img src="../../public/logo.png" alt="">
            </div>
            <div class="input-group">
                <select @change="searchGenresFilms" class="my-form-select" id="inputGroupSelect01" v-model="searchGenres">
                    <option value="">ricerca per genere</option>
                    <option v-for="(genreFilm, i) in genresFilms" :key="i" :value="genreFilm.name">{{genreFilm.name}}</option>
                </select>
                <input type="text" class="input-search" placeholder="ricerca un film per titolo" v-model="searchFilms">
                <!-- al cilck del pulasante faccio un emit verso App.vue per passare quello che l utente ha inserito nell input  -->
                <button class="btn btn-outline-secondary" type="button" @click="SearchTextFilms">Cerca</button>
            </div>
        </div>
    </header>
</template>

<script>
export default {
    data(){
        return{
            searchFilms:"",
            searchGenres:""
        }
    },
    props:{
        genresFilms: Array,
        genresSeries: Array
    },
    methods:{
        SearchTextFilms(){
            // faccio l emit dove passo una funzione e la stringa che è stata inserita dall utente 
            this.$emit("searchFilms", this.searchFilms)
        },
        searchGenresFilms(){
            this.$emit("searchGenres", this.searchGenres)
        }
    }
}
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.my-nav{
    & .nav-logo{
        & img{
            width: 150px;
        }
    }
    & .my-form-select{
        width: 200px;
        flex: none;
        margin-left: auto;
        margin-right: .5rem;
        background-color: inherit;
        color: #757575;
        border: 1px solid white;
        border-radius: 0;

        & option{
            background-color: $dark;

        }
    }
    & .input-search{
        background-color: inherit;
        color:white;
        border: 1px solid white;
        margin-right: .5rem;
        margin-left: auto;

        &:focus-visible{
            outline: none;
        }
        
    
    }

    & .btn-outline-secondary{
        border-color: white;
        color: #757575;
        &:hover{
            background-color: #313131;
        }
        
    }
}

</style>