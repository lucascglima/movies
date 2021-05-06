<template>
<v-list tree-line
  class="mx-auto"
  max-width="1200"
>
      <v-list-item-group>
      <v-card-title class="yellow--text justify-center">
          MY MOVIES
      </v-card-title>
        <template v-for="(item, index) in moviesSaved" >
          <v-list-item :key="item + [Math.random()]" >
            <template >
              <v-list-item-content 
                class="mx-6"
                 @click="action(index)"
              >
                <v-list-item-title 
                  class="yellow--text text-uppercase font-weight-medium " 
                  v-text="item.title"
                ></v-list-item-title>
                <v-list-item-subtitle 
                  class="text--primary" 
                  v-text="item.actors"
                ></v-list-item-subtitle>
                <v-list-item-action-text 
                  class="text--primary" 
                  v-text="item.genre"
                ></v-list-item-action-text>
                <v-list-item-content
                  class="text--disabled text-justify"
                  v-text="item.resume"
                ></v-list-item-content>
              </v-list-item-content>
              
            <v-overlay
              :z-index="zIndex"
              :value="overlay"
            >
              <v-card>
                <v-img
                  max-width="400"
                  :src="poster"
                ></v-img>
              </v-card>   
          </v-overlay>
            </template>
          </v-list-item>

          <v-divider
            v-if="index < moviesSaved.length - 1"
            :key="index"
          ></v-divider> 
        </template>
      </v-list-item-group>
    </v-list>    
</template>

<script>
export default {

  data: () => ({
      overlay: false,
      zIndex: 0,
      poster: null,
      star: false,
    }),

    watch: {
      overlay (val) {
        val && setTimeout(() => {
          this.overlay = false
        }, 1500)
      },
    },

    computed: {
      moviesSaved() {
        return this.$store.state.moviesSaved;
      }
    },
  methods: {
    action(index) {
      this.overlay = !this.overlay;
      this.poster = this.moviesSaved[index].poster;
    },
    favorited() {
      this.star = !this.star;
    }
  }
}
</script>

<style scoped>

</style>