<template>
    <div class="card-container">
        <!-- cicliamo l'array che  ci arriva tramite la props -->
        <div class="card" v-for="element in userFilm" :key="element.id">
           <h3 class="title">
               {{element.title}}
           </h3>
           <h5 class="sub-title">
               {{element.original_title}}
           </h5>
            <div>
                <img class="photo" :src="imgCard(element.poster_path)">
              
           </div>
           <div>
                 <img class="flags" :src="flagsNation(element.original_language)" :alt="element.original_language">
               {{element.original_language}}
           </div>
          
           <div class="vote">
               {{element.vote_average}}
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
        userFilm: Array 
    },
    methods:{
        flagsNation(nationality){
            if(nationality == 'en'){
                nationality = 'gb'
            }else if(nationality == 'ja'){
                nationality = 'jp'
            }
            return 'https://countryflagsapi.com/svg/' + nationality
            
        },

        imgCard(photo){
            return 'https:image.tmdb.org/t/p/w342' + photo
        }

    }
}
</script>

<style lang="scss" scoped>
@import '../style/common';

.card-container{
    display: flex;
    flex-wrap: wrap;
    .card{
        width: calc((100% / 5) - 8px);
        margin: 4px;
        background-color: lightcoral;
        .title, .sub-title{
            text-align: center;
            margin: 5px 2px;
        }
        .flags{
            width: 20px;
            margin: 5px 2px;

        }

        .photo{
            max-width: 300px;
            max-height: 300px;
            overflow: hidden;
        }
    }
}
</style>