<template>
  <div class="search" :class="{ hasResults }">
    <h1>{{ heading }}</h1>
    <v-container grid-list-md text-xs-center>
      <v-layout row wrap>
        <v-flex xs10>
          <v-text-field
            color="white"
            label="Search recipe"
            class="input-group--focused"
            v-model="keyword"
            v-on:keyup.enter="handleSearch"
            dark
          ></v-text-field>
        </v-flex>
        <v-flex xs2>
          <v-btn
            flat
            outline
            large
            color="white"
            type="submit"
            v-on:click="handleSearch"
          >Search</v-btn>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'Search',
  props: ['search', 'hasResults'],
  data() {
    return {
      heading: 'Search!',
      keyword: null,
    };
  },
  methods: {
    handleSearch() {
      this.$emit('search', this.keyword);
    },
  },
};
</script>

<style scoped>
  .search h1 {
    color: #fff;
    font-size: 40px;
    text-transform: uppercase;
  }
  .search {
    text-align: center;
    padding-top: 200px;
    transition: padding-top .5s;
  }
  .search.hasResults {
    padding-top: 5px;
  }
</style>
