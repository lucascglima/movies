<template> 
  
  <v-container>
      <v-card
        class="mx-auto"
        max-width="500"
      >
      <v-text-field
        label="Escolha seu filme"
        color="indigo darken-1 "
        v-model="inputMovie"
        type="input"
      ></v-text-field>

        <v-card-title class="font-weight-bold"> 
          Title: {{movie.Title}}
        </v-card-title>

        <v-card-subtitle class="py-0">
          Resume: {{movie.Plot}}
        </v-card-subtitle>

        <v-card-text class="text--primary">
          <div class="py-6">Actors: {{movie.Actors}}</div>

          <div>Genre: {{movie.Genre}}</div>

          <div>Director: {{movie.Director}}</div>
        </v-card-text>
        <v-img
          max-width="500"
          :src="movie.Poster"
        >   
        </v-img>
      </v-card>

  </v-container>

  
    
</template>

<script>
import axios from "axios";

const urlMovies = 'http://www.omdbapi.com/';
const apiKey = '&apikey=87a9386d';

  export default {

    data: () => ({
      movie: "",
      inputMovie: "",
    }), 
    mounted () {
  
        // const urlBatman = urlMovies + "?t=" + "this.inputMovie" + "&apikey" + apiKey;
        // axios
        // .get(urlBatman)
        // .then ( bat => (this.batman = bat.data))
  
      // axios
      // .get('http://www.omdbapi.com/?t=batman&apikey=87a9386d')
      // .then(response => (this.batman = response.data));

      // axios
      // .get('http://www.omdbapi.com/?t=avengers&apikey=87a9386d')
      // .then (res => (this.avengers = res.data))
    },

    watch: {
      inputMovie() {
        const urlMovie = urlMovies + "?t=" + this.inputMovie + "&plot=full&apikey" + apiKey;
        axios
        .get(urlMovie)
        .then ( bat => (this.movie = bat.data))
        
      }
    }

  }
</script>
