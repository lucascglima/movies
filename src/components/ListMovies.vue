<template>
<v-list tree-line>
      <v-list-item-group
        active-class="yellow--text"
        multiple
      >
      <v-card-title class="yellow--text justify-center">
          MY MOVIES
      </v-card-title>
        <template v-for="(item, index) in moviesSaved">
          <v-list-item :key="item.title">
            <template v-slot:default="{ active }">
              <v-list-item-content>
                <v-list-item-title v-text="item.title"></v-list-item-title>

                <v-list-item-subtitle
                  class="text--primary text-justify"
                  v-text="item.resume"
                ></v-list-item-subtitle>

                <v-list-item-subtitle v-text="item.actors"></v-list-item-subtitle>
              </v-list-item-content>

              <v-list-item-action>
                <v-list-item-action-text v-text="item.genre"></v-list-item-action-text>
                

                <v-icon
                  v-if="!active"
                  color="grey lighten-1"
                >
                  mdi-star-outline
                </v-icon>

                <v-icon
                  v-else
                  color="yellow darken-3"
                >
                  mdi-star
                </v-icon>
              </v-list-item-action>
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


    computed: {
      moviesSaved() {
        return this.$store.state.moviesSaved;
      }
    },
}
</script>

<style scoped>

</style>