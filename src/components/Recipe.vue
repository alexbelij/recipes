<template>
  <v-flex d-flex xs12 sm6 md4>
    <v-card>
      <v-card-media :src="recipe.image" height="200px">
      </v-card-media>
      <v-card-title primary-title>
        <div>
          <h3 class="headline mb-0">{{ recipe.label }}</h3>
          <span class="grey--text">By {{ recipe.source }}</span>
        </div>
      </v-card-title>
      <v-chip
        v-for="tag in recipe.healthLabels"
        :key="tag"
        small
      >
        {{ tag }}
      </v-chip>
      <v-card-actions>
        <v-btn flat color="teal darken-3" v-on:click="showDetail(recipe)">See Detail</v-btn>
      </v-card-actions>
    </v-card>
  </v-flex>
</template>

<script>
export default {
  name: 'Recipe',
  props: ['recipe', 'showDetail'],
};
</script>

<style scoped>
  .recipe {
    border: solid 1px #fff;
    transition: all .5s;
  }
  .recipe img {
    max-height: 150px;
    float: left;
  }
  .recipe p {
    padding: 10px;
  }
</style>
