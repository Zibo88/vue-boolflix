<template>
    <div class="card-container">
        <!-- cicliamo l'array che  ci arriva tramite la props -->
        <h2>Film</h2>
        <div class="film-container flex">
            <div class="card" v-for="element in userFilm" :key="element.id">
                <!-- img -->
                <div class="poster">
                    <img class="photo" :src="imgCard(element.poster_path)" :alt="element.poster_path" >
                </div>
                <div class="element-hover-container flex">
                    <!-- title -->
                    <h3 class="title">
                    Titolo: {{element.title}}
                    </h3>
                    <!-- sub-title -->
                    <h5 class="sub-title">
                        Titolo originale: {{element.original_title}}
                    </h5>
                <!-- flags -->
                    <div>
                        <img class="flags" :src="flagsNation(element.original_language)" :alt="element.original_language">
                        <!-- {{element.original_language}} -->
                    </div>
                    <!-- vote -->
                    <div class="vote" :class="voteStar(element.vote_average)">
                        <i class="fa-star" :class="(star <= voteStar(element.vote_average)) ? 'fa-solid' : 'fa-regular'" v-for="star in 5 " :key="star"></i>
                    
                    </div>
                    
                    <div class="overview">
                        {{element.overview}}
                    </div>
                </div>
            </div>
        </div>
        
            <!-- serie -->
            <h2>Serie TV</h2>
            <div class="container-series flex">
                <div class="card" v-for="element in userSeries" :key="element.id">
                <!-- img -->
                <div class="poster">
                    <img class="photo" :src="imgCard(element.poster_path)" :alt="element.poster_path" >
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
            }
            return 'https://countryflagsapi.com/svg/' + nationality
            
        },

        imgCard(photo){
            return 'https:image.tmdb.org/t/p/w342' + photo
        },

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

.card-container{
    overflow: hidden;
    .film-container.flex, .container-series.flex{
        width: 100vw;
        overflow-x: auto;
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
            width: 400px;
            height: 400px;
            overflow: hidden;
        }

        .element-hover-container.flex{
            width: 100%;
            height: 100%;
            position: absolute;
            top: 0;
            left: 0;
            color: white;
            background-color: black;
            flex-direction: column;
            display: none;

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