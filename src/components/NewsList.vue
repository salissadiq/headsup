<template>
  <div>
    <ul>
      <li v-for="(article, index) in articles" :key="index">
        <img height="180" width="250" :src="article.urlToImage" />
        <h3>{{article.title}}</h3>
        <h5>Date: {{article.publishedAt}}</h5>
        <h6 v-if="article.author">By: {{article.author}}</h6>
        <h6 v-else>Ananymous</h6>
        <code>{{article.source.name | truncate(20)}}</code>
        <p>Description: {{article.description}}</p>
        <p>{{article.content}}</p>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: ["articles"]
};
</script>
<style scoped>
* {
  font-family: "Merriweather", serif;
  margin: 0;
  padding: 0;
}

div {
  margin: 20px;
}

ul {
  list-style-type: none;
}

h3 {
  font: bold 20px/1.5 Helvetica, Verdana, sans-serif;
}

li img {
  float: left;
  margin: 0 15px 0 0;
}

li p {
  font: 200 12px/1.5 Georgia, Times New Roman, serif;
}

li {
  padding: 10px;
  overflow: auto;
}

li:hover {
  background: #eee;
  cursor: pointer;
}
</style>