<template>
    <header class="pt-3">
        <div class="container">
            <div class="input-group mb-3">
                <input type="text" class="form-control" placeholder="ricerca un film" v-model="searchFilms">
                <!-- al cilck del pulasante faccio un emit verso App.vue per passare quello che l utente ha inserito nell input  -->
                <button class="btn btn-outline-secondary" type="button" @click="onSearchFilms">Cerca</button>
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
        onSearchFilms(){
            // faccio l emit dove passo una funzione e la stringa che è stata inserita dall utente 
            this.$emit("searchFilms", this.searchFilms)
        }
    }
}
</script>

<style lang="scss" scoped>

</style>