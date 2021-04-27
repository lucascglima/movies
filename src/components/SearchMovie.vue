<template> 
  
  <v-container class=" mt-6">
      <v-card
        class="mx-auto "
        max-width="1200"
      >
      <v-row class="mx-4 mt-4 d-flex">
        <v-text-field
          label="Search Movies"
          color="yellow"
          v-model="inputMovie"
          type="input"
          class="yellow--text mx-8 "
          @keyup.enter="save()"
      >
      </v-text-field>
      <v-btn 
        class="my-4 yellow darken-1 blue-grey--text"
        @click="save()"
      >
        Save
      </v-btn>

      <v-btn
        class="my-4 ml-1 yellow darken-1 blue-grey--text"
      >
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
      </v-row>
        
      <v-row class="mx-4 d-flex">
        <v-col>
        <v-card-title class=" text-center"> 
          <span class=" yellow--text py-1 px-1 rounded "> Movie: {{movie.Title}}</span>
          
        </v-card-title>
        <v-card-text class="font-weight-Light white-white--text">
          <p class="py-1" >
           <span class=" yellow--text py-1 px-1 rounded font-weight-medium">Resume:</span> {{movie.Plot}}
          </p>
          <p class="py-1">
            <b class=" yellow--text py-1 px-1 rounded">Actors:</b> {{movie.Actors}}
          </p>

          <p class="py-1">
           <b class=" yellow--text py-1 px-1 rounded"> Genre:</b> {{movie.Genre}}
          </p>

          <p class="py-1">
           <b class=" yellow--text py-1 px-1 rounded"> Director: </b> {{movie.Director}}
          </p>
        </v-card-text>
        </v-col>
        <v-img
          max-width="400"
          :src="movie.Poster"
          class="mr-4"
          v-model="movieImg"
        > 
        </v-img>
            </v-row>
      </v-card>
      <ListMovies/>
  </v-container>   
</template>

<script>
import axios from "axios";
import ListMovies from "./ListMovies"

const urlMovies = 'http://www.omdbapi.com/';
const apiKey = '&apikey=87a9386d';

  export default {

    data: () => ({
      movie: "",
      inputMovie: "",
    }),

    components: {
      ListMovies,
    },

    computed: {
      moviesSaved() {
        return this.$store.state.moviesSaved;
      }
    },
    watch: {
      inputMovie() {
        const urlMovie = urlMovies + "?t=" + this.inputMovie + "&plot=full&apikey" + apiKey;
        axios
        .get(urlMovie)
        .then ( bat => (this.movie = bat.data))
        
      }
    },
    methods: {
      save() {
        if(this.inputMovie != "") {
          //Get Atributes from object movie
          this.moviesSaved.push({
          title:this.movie.Title,
          actors:this.movie.Actors,
          resume:this.movie.Plot,
          genre: this.movie.Genre,
          director:this.movie.Director,
          poster: this.movie.Poster,
          })
          console.log(this.moviesSaved);
          this.inputMovie = "";  
          this.movieImg.width="0";   
          }
          else {
            alert("Choose a movie")
          }
          
        }
        
      }
  }
</script>
