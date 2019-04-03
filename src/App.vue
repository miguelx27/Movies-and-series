<template>
  <div id="app">
    <Header @search="search"/>
    <div v-if="results.totalResults.length">
      <h1>{{ results.totalResults }} Results for "{{ results.query}}"</h1>
      <ListItem :items="results.Search" />
      <v-pagination :length="results.pages" v-model="page"></v-pagination>
    </div>
    <h1 v-else>No results found</h1>
  </div>
</template>

<script>
import ListItem from './components/ListItem.vue';
import axios from 'axios';
import Header from './components/Header.vue';
import './css/main.css';

export default {
  name: 'app',
  data() {
    return {
      results: {Search: [], totalResults: 0, query: ''},
      page: 1,
      lastSearch: { query: '', type: '' },
    };
  },

  components: {
    Header,
    ListItem
  },

  methods:{
    async search(query){
      try {
        this.page = 1;
        const results = await axios.get(`https://www.omdbapi.com/?type=${query.type}&s=${query.query}&page=${this.page}&i=tt3896198&apikey=b0c91d0c`);

        if (results.data.Response == 'True') {
          this.results = results.data;
          this.results.pages = Math.ceil(results.data.totalResults / 10);
          this.results.query = query.query;

          this.lastSearch = query;
        } else {
          this.results = {Search: [], totalResults: 0, query: '', pages: 0};  
        }

      } catch (e) {
        this.results = {Search: [], totalResults: 0, query: '', pages: 0};
      }
        
    }

   },

   watch: {
    async page() {
      try {
        const results = await axios.get(`https://www.omdbapi.com/?type=${this.lastSearch.type}&s=${this.lastSearch.query}&page=${this.page}&i=tt3896198&apikey=b0c91d0c`);

        if (results.data.Response == 'True') {
          this.results = results.data;
          this.results.pages = Math.ceil(results.data.totalResults / 10);
        } else {
          this.results = {Search: [], totalResults: 0, query: '', pages: 0};  
        }

      } catch (e) {
        this.results = {Search: [], totalResults: 0, query: '', pages: 0};
      }
    }
   }
}

</script>

<style>
#app {
  height: 100%;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
