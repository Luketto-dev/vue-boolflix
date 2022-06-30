<template>
    <header class="py-2 px-5 bg-dark">
        <div class="my-nav d-flex">
            <div class="nav-logo">
                <img src="../../public/logo.png" alt="">
            </div>
            <div class="input-group">
                <input type="text" class="input-search" placeholder="ricerca un film" v-model="searchFilms">
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
        }
    },
    methods:{
        SearchTextFilms(){
            // faccio l emit dove passo una funzione e la stringa che è stata inserita dall utente 
            this.$emit("searchFilms", this.searchFilms)
        }
    }
}
</script>

<style lang="scss" scoped>

.my-nav{
    & .nav-logo{
        & img{
            width: 150px;
        }
    }
    & .input-search{
        background-color: inherit;
        color:white;
        border: 1px solid white;
        margin-right: .5rem;
        margin-left: auto;
    }

    & .btn-outline-secondary{
        border-color: white;
        color: white;
        &:hover{
            background-color: #313131;;
        }
    }
}

</style>