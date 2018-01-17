<template>
  <div class="recipes">
    <search v-bind="{search, query, hasResults}" v-on:search="search"></search>
    <ul>
      <v-container fluid grid-list-xl>
        <v-layout row wrap v-scroll="onScroll">
          <recipe
            v-for="recipe in recipes"
            :key="recipe.message"
            v-bind="{recipe, showDetail}"
          ></recipe>
        </v-layout>
      </v-container>
      <v-progress-circular
        v-if="loading"
        indeterminate
        v-bind:size="70"
        color="white"
      ></v-progress-circular>
    </ul>
    <detail :show="recipe.image" :recipe="recipe"></detail>
  </div>
</template>

<script>
import config from '../config';
import Recipe from './Recipe';
import Search from './Search';
import Detail from './Detail';

export default {
  name: 'Recipes',
  components: {
    Recipe,
    Search,
    Detail,
  },
  data() {
    return {
      loading: false,
      query: '',
      from: 0,
      to: 10,
      recipes: [],
      recipe: {},
    };
  },
  methods: {
    search(keyword) {
      if (keyword && keyword.length) {
        this.reset();
        this.query = keyword;
        this.loadData(this.query, this.from, this.to);
      }
    },
    loadData(query, from = 0, to = 10) {
      this.loading = true;
      fetch(`${config.url}?app_id=${config.appId}&app_key=${config.appKey}&q=${query}&from=${from}&to=${to}`)
        .then(res => res.text())
        .then((text) => {
          const data = JSON.parse(text) || [];
          if (data.hits && data.hits.length) {
            data.hits.forEach((hit) => {
              this.recipes.push(hit.recipe);
            });
            console.log(data.hits);
          }
          this.loading = false;
        }).catch((err) => {
          console.error(err);
          this.loading = false;
        });
    },
    reset() {
      this.recipes = [];
      this.recipe = {};
      this.from = 0;
      this.to = 10;
    },
    showDetail(recipe) {
      this.recipe = recipe;
    },
    onScroll() {
      const scrollTop = document.documentElement.scrollTop;
      const windowHeight = window.innerHeight;
      const bodyHeight = document.documentElement.offsetHeight - windowHeight;
      const scrollPercentage = (scrollTop / bodyHeight);
      // if the scroll is more than 90% from the top, load more content.
      if (scrollPercentage > 0.9) {
        this.from += 10;
        this.to += 10;
        // this.loadData(this.query, this.from, this.to);
      }
    },
  },
  computed: {
    hasResults() {
      return this.recipes.length;
    },
  },
};
</script>

<style>
  body {
    height: 100%;
    margin: 0;
    font-family: Verdana, sans-serif;
  }
  #app {
    width: 100%;
    height: 100%;
    background-color: #41B883;
    background: linear-gradient(to right, #41B883, #35495E);
  }
  .recipes {
    margin: 10px;
    text-align: center;
  }
  .recipes > ul {
    list-style: none;
    padding: 10px;
    width: 60%;
    margin: 0 auto;
    color: #fff;
  }
</style>
