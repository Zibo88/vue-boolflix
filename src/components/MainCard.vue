<template>
    <div class="card-container">
        <!-- cicliamo l'array che  ci arriva tramite la props -->
        <div class="card" v-for="element in userFilm" :key="element.id">
           <h3 class="">
               {{element.title}}
           </h3>
           <h5>
               {{element.original_title}}
           </h5>
            <div>
                <img class="photo" :src="imgCard(element.poster_path)">
              
           </div>
           <div>
                 <img class="flags" :src="flagsNation(element.original_language)">
               {{element.original_language}}
           </div>
          
           <div>
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
        width: calc((100% / 6) - 8px);
        margin: 4px;

        .flags{
            width: 20px;

        }

        .photo{
            max-width: 150px;
            max-height: 150px;
            overflow-y: hidden;
        }
    }
}
</style>