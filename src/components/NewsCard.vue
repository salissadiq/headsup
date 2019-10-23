<template>
  <v-row class="fill-height">
    <template v-for="(article, i) in articles">
      <v-col :key="i" cols="12" md="4">
        <template>
          <v-card class="mx-auto" max-width="344" outlined>
            <v-list-item three-line>
              <v-list-item-content>
                <div class="overline mb-4">
                  {{article.title | truncate(45)}}
                  <br />
                  {{article.publishedAt}}
                </div>
                <v-list-item-title
                  v-if="article.author"
                  class="headline mb-1"
                >{{article.author | truncate (10)}}</v-list-item-title>
                <v-list-item-title v-else class="headline mb-1">Ananymous</v-list-item-title>
                <v-list-item-subtitle>{{article.description }}</v-list-item-subtitle>
                <v-list-item-subtitle>
                  <code>{{article.source.name | truncate(20)}}</code>
                </v-list-item-subtitle>
              </v-list-item-content>

              <v-list-item-avatar tile size="100">
                <v-img v-if="article.urlToImage" :src="article.urlToImage"></v-img>
                <v-img v-else :src="article.urlToImage"></v-img>
              </v-list-item-avatar>
            </v-list-item>

            <v-card-actions>
              <v-btn color="error" dark text @click="goTo(article.url)">Read</v-btn>
            </v-card-actions>
          </v-card>
        </template>
      </v-col>
    </template>
  </v-row>
</template>
<script>
export default {
  props: ["articles"],
  methods: {
    goTo(url) {
      window.open(url);
    }
  }
};
</script>