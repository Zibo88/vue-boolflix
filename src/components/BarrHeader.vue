<template>
    <div class="container-header flex">
        <div class="logo">
            <h1>
                BOOLFLIX
            </h1>
        </div>
        
        <div class="search-barr">
             <!-- leggo il valore inserito dall'utente e lo salvo nella variabile userChoice -->
            <!-- tramite il @keyup.enter invio l'emit al padre App.vue (userfilm è l'ancoraggio che riporterò poi in app.vue mentre userChoice è la variabile di cui necessita per funzionare) -->
            <input v-model="userChoice" @keyup.enter="$emit('userFilm', userChoice )" placeholder="cerca il tuo film" type="text">
        </div>
       
    </div>
</template>

<script>
export default {
    name: 'BarrHeader',
    data(){
        return{
            userChoice: '',
        }  
    }
    
}
</script>

<style lang="scss" scoped>
@import '../style/common';
.container-header{
    background-color: black;
    justify-content: space-between;
    align-items: center;
    padding: 10px;

    h1{
        color: red;
    }
}

</style>