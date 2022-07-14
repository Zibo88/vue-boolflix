<template>
    <div class="app-container">
        <BarrHeader @userFilm='choiceUser'/>
      
         <!-- utilizzo il componente e lo passo al figlio MainCard tramite una props, come valore do l'array riempito tramite la chiamata axios -->
          <MainCard :userFilm='arrayFilm' :userSeries='arraySerie'/>
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
        // l'url è composto da una parte fissa fino  query= che viene implementata ogni volta che viene eseguita una chiamata axios con questo parametro (this.urlFilms + word)
        urlFilms:'https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=',
        arraySerie: [],
        urlSeries:'https://api.themoviedb.org/3/search/tv?api_key=e99307154c6dfb0b4750f6603256716d&language=it_IT&query=',
    
    }     
  },
  components: {
    BarrHeader,
    MainCard
  },
   
  methods:{
    // word è il parametro che in questo caso è uguale alla variabile (UserChoice) passata con $emit da BarrHeader con il nome di ancoraggio @userFilm perchè l'ancoraggio adesso avrà valore del metodo assegnato
    choiceUser(word){
      console.log('word',word)

  // eseguo la chiamata axios, e come parametro utilizzo l'url dei film + la parola scelta dall'utente (UserChoice)
      axios.get(this.urlFilms + word).then((response) =>{
        // il console log di response ci permette di visualizzare il contenuto della chiamata axios
        console.log('tutti i dati', response)
        // il risultato della chiamata lo assegno all'array vuoto, response.data.results in questo caso rappresenta il luogo dove si trovano i dati.
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
@import './style/common';

.app-container{
  height: 100vh;
}
</style>

