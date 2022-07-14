<template>
    <div class="card-container">
        
        <h2 class="tipolgy">Film</h2>
        <div class="film-container flex">
             <!-- cicliamo l'array che  ci arriva tramite la props userSeries-->
            <div class="card" v-for="element in userFilm" :key="element.id">
                <!-- img -->
                <div class="poster">
                    <!-- se è presente element.poster_path stampalo/ l'img è data dal path + element.poster_path --> 
                    <img v-if="element.poster_path" class="photo" :src="imgCard(element.poster_path)" :alt="element.poster_path" >
                    <!-- altrimenti stampa -->
                    <img v-else class="photo" :src="'https://cdn1.vectorstock.com/i/1000x1000/21/35/404-error-page-or-file-not-found-icon-file-vector-21212135.jpgf'">
                </div>
                <div class="element-hover-container flex">
                    <!-- title -->
                    <h3 class="title" >
                    Titolo: {{element.title}}
                    </h3>
                    <!-- sub-title -->
                    <h5 class="sub-title">
                        Titolo originale: {{element.original_title}}
                    </h5>
                <!-- flags -->
                    <div>
                        <img class="flags" :src="flagsNation(element.original_language)" :alt="element.original_language">
                    </div>
                    <!-- vote -->
                     <!-- eseguo un ciclo v for per stampare le 5 stelle -->
                        <!-- insericìsco un classe dinamica che mi permette di modificare l'icona in base al valore del voto. Star che è l'elemento ciclato è inferiore/uguale al voto ? la classe è solid, : se no è regular -->
                    <div class="vote" :class="voteStar(element.vote_average)">
                        <i class="fa-star" :class="(star <= voteStar(element.vote_average)) ? 'fa-solid' : 'fa-regular'" v-for="star in 5 " :key="star"></i>
                    </div>
                    <!-- overview -->
                    <div class="overview">
                        {{element.overview}}
                    </div>
                </div>
            </div>
        </div>
        
            <!-- serie -->
        <h2 class="tipolgy">Serie TV</h2>
        <div class="container-series flex">
            <!-- eseguo un ciclo for nell'array passato tramite propos  -->
            <div class="card" v-for="element in userSeries" :key="element.id">
                <!-- img -->
                <div class="poster">
                    <img v-if="element.poster_path" class="photo" :src="imgCard(element.poster_path)" :alt="element.poster_path" >
                    <img v-else class="photo" :src="'https://cdn1.vectorstock.com/i/1000x1000/21/35/404-error-page-or-file-not-found-icon-file-vector-21212135.jpg'">
                </div>
                <div class="element-hover-container flex">
                    <!-- title -->
                    <h3 class="title">
                    Titolo: {{element.name}}
                    </h3>
                    <!-- sub-title -->
                    <h5 class="sub-title">
                        Titolo originale: {{element.original_name}}
                    </h5>
                    <!-- flags -->
                    <div>
                        <!-- aggiiungo la funzione flagsNation al :src e do come valore la lingua originale -->
                        <img class="flags" :src="flagsNation(element.original_language)" :alt="element.original_language">
                    </div>
                    <!-- vote -->
                    <div class="vote"  >
                        <!-- eseguo un ciclo v for per stampare le 5 stelle -->
                        <!-- insericìsco un classe dinamica che mi opermette di modificare l'icona in base al valore del voto. Star che è l'elemento ciclato è inferiore/uguale al voto ? la classe è solid, : se no è regular -->
                        <i class="fa-star" :class="(star <= voteStar(element.vote_average)) ? 'fa-solid' : 'fa-regular'" v-for="star in 5 " :key="star"></i>
                        <!-- {{element.vote_average}} -->
                    </div>
                    <!-- overview -->
                    <div class="overview">
                        {{element.overview}}
                    </div>
                </div>    
            </div>
        </div>
    </div>
   
</template>



<script>

// import axios from 'axios'

export default {
    name: 'MainCard',
    props: {
        // props che origina dal padre App.vue, passiamo un array 
        userFilm: Array, 
        userSeries: Array,
    },
    methods:{
        flagsNation(nationality){
            if(nationality == 'en'){
                nationality = 'gb'
            }else if(nationality == 'ja'){
                nationality = 'jp'
            }else if (nationality == 'cs'){
                nationality = 'cz'
            }else if (nationality == 'ko'){
                nationality = 'kr'
            }else if (nationality == 'hi'){
                nationality = 'in'
            }else if (nationality == 'zh'){
                nationality = 'cn'
            }
            return 'https://countryflagsapi.com/svg/' + nationality
            
        },

        // funzione che richiama il path delle foto e aggiunge il singolo poster_path
        imgCard(photo){
            return 'https:image.tmdb.org/t/p/w342' + photo
        },

        // funzione che arrotonda il voto dato al film per eccesso
        voteStar(vote){
            let voters = Math.ceil(vote/2) 
            console.log('voti',voters)
            return voters
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../style/common';
@import '../style/variables';

.card-container{
    height: calc(100vh - 90px);
    overflow: hidden;
    .film-container.flex, .container-series.flex{
        width: 100vw;
        overflow-x: auto;
    }
    .tipolgy{
        margin-left: 10px;
        font-size: 30px;
        color: white;
    }
    .card{
        margin: 8px;
        position: relative;
        
        .title, .sub-title{
            margin: 5px 2px;
        }
        .flags{
            width: 20px;
            margin: 10px 2px;
        }

        .vote{
            margin: 10px 2px;
            i{
                color: yellow;
            }
        }

        .poster{
            width: 250px;
            height: 250px;
            overflow: hidden;
        }

        .element-hover-container.flex{
            width: 100%;
            height: 100%;
            position: absolute;
            top: 0;
            left: 0;
            color: white;
            background-color: rgba(black, 0.7);
            opacity: 1;
            flex-direction: column;
            display: none;
            border: 2px solid lightgray;

            .overview{
                flex-grow: 1;
                padding: 5px 2px;
            }
        }

        &:hover  .element-hover-container.flex{
            display: block;
             overflow-y:auto;
        }

    }
}
</style>