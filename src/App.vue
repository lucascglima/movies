
<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      app
    >
    <v-list>
        <v-list-item
          v-for="[icon, text] in links"
          :key="icon"
          link
        >
          <v-list-item-icon >
            <v-icon 
              color="yellow darken-1"
            >{{ icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="yellow--text">{{ text }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"
       color="yellow darken-1"
      ></v-app-bar-nav-icon>

      <v-toolbar-title
         color="yellow--text"
      >LKS</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <SearchMovie></SearchMovie>
    </v-main>
  </v-app>
</template>

<script>
import SearchMovie from './components/SearchMovie'

export default {


  data: () => ({
    drawer: null,
    links: [
        ['mdi-movie', 'Movies'],
        ['mdi-star', 'Favorites'],
        ['mdi-delete', 'Excluded'],
        ['mdi-alert-octagon', 'Spam'],
    ]
  }),

  components: {
    SearchMovie,

  }
};
</script>
<style>

</style>