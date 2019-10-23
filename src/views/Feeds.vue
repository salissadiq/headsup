<template>
  <v-container class="pa-4">
    <form @submit.prevent="searchNews">
      <v-col cols="12" lg="12">
        <v-text-field v-model="keyWord" @blur="searchNews" label="Search Here" outlined shaped></v-text-field>
        <v-progress-linear v-if="loading" indeterminate color="green"></v-progress-linear>
      </v-col>
    </form>
    <div class="text-center">
      <v-btn class="mx-2" @click="grid = true " fab dark color="teal">
        <v-icon dark>mdi-format-list-bulleted-square</v-icon>
      </v-btn>
      <v-btn color="teal" @click="grid = false" fab dark>
        <v-icon>mdi-domain</v-icon>
      </v-btn>
    </div>
    <NewsList v-if="grid" :articles="articles" />
    <NewsCard v-else :articles="articles" />
    <center>
      <v-btn class="ma-2" dark justify="center" color="error" @click="scroll">
        Load More
        <v-icon>mdi-arrow-down</v-icon>
      </v-btn>
    </center>
  </v-container>
</template>

<script>
import NewsCard from "../components/NewsCard";
import NewsList from "../components/NewsList";
export default {
  components: {
    NewsCard,
    NewsList
  },
  computed: {
    pageCount() {
      return Math.ceil(this.totalResults / this.maxPerPage);
    }
  },
  data() {
    return {
      apiKey: "7cc1cb81583e40848c40b32ad061a385",
      url: null,
      loading: false,
      showloader: false,
      currentPage: 1,
      totalResults: 0,
      maxPerPage: 20,
      keyWord: null,
      articles: [],
      country: "us",
      grid: false
    };
  },
  methods: {
    resetData() {
      this.currentPage = 1;
      this.articles = [];
    },
    searchNews() {
      if (this.keyWord !== "") {
        this.url = `https://newsapi.org/v2/everything?q=${this.keyWord} &pageSize=${this.maxPerPage}&apiKey=${this.apiKey}`;
        this.loading = true;
        this.resetData();
        this.fetchData();
      } else {
        this.fetchTopNews;
      }
    },
    fetchTopNews() {
      this.url = `https://newsapi.org/v2/top-headlines?country=${this.country}&pageSize=${this.maxPerPage}&apiKey=${this.apiKey}`;
      this.loading = true;
      this.searchWord = "";
      this.resetData();
      this.fetchData();
    },
    fetchData() {
      let req = new Request(`${this.url}&page=${this.currentPage}`);
      fetch(req)
        .then(resp => resp.json())
        .then(data => {
          console.log(data);
          // this.totalResults = data.totalResults;
          data.articles.forEach(element => {
            this.articles.push(element);
          });
          this.loading = false;
          this.showloader = false;
        })
        .catch(error => {
          console.log(error);
        });
    },
    scroll() {
      this.currentPage++;
      let req = new Request(`${this.url}&page=${this.currentPage}`);
      fetch(req)
        .then(resp => resp.json())
        .then(data => {
          console.log(data);
          // this.totalResults = data.totalResults;
          data.articles.forEach(element => {
            let newData = this.articles.concat(element);
            this.articles = newData;
          });
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  created() {
    this.fetchTopNews();
  }
};
</script>
<style scoped>
</style>