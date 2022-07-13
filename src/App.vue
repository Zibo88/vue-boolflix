<template>
    <div>
      
        <BarrHeader @userFilm='choiceFilm'/>
       <div>
         <!-- utilizzo il componente e lo passo al figlio MainCard tramite una props, come valore do l'array riempito tramite la chiamata axios -->
          <MainCard :userFilm='arrayFilm' :userSeries='arraySerie'/>
      </div>
    </div>

   
</template>

<script>

import BarrHeader from './components/BarrHeader.vue'
import MainCard from './components/MainCard.vue'
import axios from 'axios'

export default {
 
  name: 'App',
  data(){
    return{
        arrayFilm: [],
        urlFilms:'https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=',
        // fai un altro componenete
        arraySerie: [],
        urlSeries:'https://api.themoviedb.org/3/search/tv?api_key=e99307154c6dfb0b4750f6603256716d&language=it_IT&query=',
    
    }     
  },
  components: {
    BarrHeader,
    MainCard
  },
   
  methods:{
    choiceFilm(word){
      console.log('word',word)

  // eseguo la chiamata axios
      axios.get(this.urlFilms + word).then((response) =>{
        // il risultato della chiamata lo assegno all'array vuoto
        this.arrayFilm = response.data.results
        console.log('arrayfilm',  this.arrayFilm)

      })

      // chiamata axios per le serie
      axios.get(this.urlSeries + word).then((response) => {
      // il risultato della chiamata lo assegno all'array vuoto
      this.arraySerie = response.data.results
      console.log('arrayserie', this.arraySerie)
        
      })
      
  },
    
  }

}

</script>

<style lang="scss">

</style>

