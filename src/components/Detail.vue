<template>
  <v-dialog
    v-model="show"
    fullscreen
    transition="dialog-bottom-transition"
    :overlay="false"
    scrollable
  >
    <v-card>
      <v-toolbar style="flex: 0 0 auto;" dark color="teal darken-3">
        <v-btn icon @click.native="show = false" dark>
          <v-icon>close</v-icon>
        </v-btn>
        <v-toolbar-title>Recipe Detail</v-toolbar-title>
      </v-toolbar>

      <v-card-media
        :src="recipe.image"
        height="250px"
      >
        <v-container fill-height fluid>
          <v-layout fill-height>
            <v-flex xs12 align-end flexbox>
              <h1 class="headline white--text" v-text="recipe.label"></h1>
              <span class="white--text">By {{ recipe.source }}</span>
            </v-flex>
          </v-layout>
        </v-container>
      </v-card-media>

      <v-card-text>
        <v-list>
          <v-subheader>Ingredients</v-subheader>
          <v-list-tile v-for="ingredient in recipe.ingredientLines" :key="ingredient">
            <v-list-tile-content>
              <v-list-tile-title>- {{ ingredient }}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-card-text>

      <v-divider></v-divider>

      <v-card-actions>
        <v-btn dark color="teal darken-3" :href="recipe.url" target="_blank"><v-icon dark>open_in_new</v-icon>&nbsp; Go to Preparation</v-btn>
      </v-card-actions>

      <div style="flex: 1 1 auto;"></div>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: 'Detail',
  props: ['show', 'recipe'],
};
</script>

<style scoped>
</style>
