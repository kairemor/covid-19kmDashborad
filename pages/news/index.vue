<template>
  <v-container fill-height fluid grid-list-xl>
    <v-layout wrap>
      <div v-for="(article, index) in articles" :key="index">
        <v-flex sm6 xs12 md6 lg6>
          <a :href="article.link" target="_blank">
            <v-card class="mx-auto" max-width="400">
              <v-img
                class="white--text align-end"
                height="200px"
                src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
              >
                <v-card-title>{{ article.title.substring(10) }}</v-card-title>
              </v-img>
              <v-card-text class="text--primary">
                <div>{{ article.title }}</div>
              </v-card-text>
            </v-card>
          </a>
        </v-flex>
      </div>
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