<template>
    <div class="container-header flex">
        <div class="logo">
            <h1>
                BOOLFLIX
            </h1>
        </div>
        
        <div class="search-barr">
             <!-- leggo il valore inserito dall'utente e lo salvo nella variabile userChoice -->
            <!-- tramite il @click sul button invio l'emit al padre App.vue (userfilm è l'ancoraggio che riporterò poi in app.vue mentre userChoice è la variabile di cui necessita per funzionare) -->
            <input class="search-input" v-model="userChoice"  placeholder="cerca il tuo film" type="text">
            <button @click="$emit('userFilm', userChoice )">Cerca</button>
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
@import '../style/variables';

.container-header{
    background-color: black;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    height: 70px;
    h1{
        color: $second_color;
    }

    .search-input{
        margin-right: 10px;
        padding: 5px;
        border-radius: 16px;
        border: 2px solid $second_color;
        background-color: whitesmoke; 
    }

    button{
        padding: 5px;
        border-radius: 16px;
        border: 2px solid $second_color;
        cursor: pointer;
    }
}

</style>