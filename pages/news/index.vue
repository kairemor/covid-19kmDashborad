<template>
  <v-container fluid grid-list-xl>
    <v-layout wrap>
      <v-flex sm xs12 md3 lg3 v-for="(article, index) in articles" :key="index">
        <a :href="article.link" target="_blank">
          <v-card>
            <v-card-text class="text--primary">
              <div>{{ article.title }}</div>
            </v-card-text>
          </v-card>
        </a>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  layout: "dashboard",
  async asyncData() {
    const { data } = await axios.get(
      `http://covid19-news.herokuapp.com/api/covid19/news`
    );
    return { articles: data.data };
  }
};
</script>