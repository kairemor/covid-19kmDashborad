<template>
  <v-container fluid grid-list-xl>
    <v-layout wrap>
      <v-flex sm xs12 md3 lg4 v-for="(faq, index) in faqs" :key="index">
        <v-card class="mx-auto" max-width="344">
          <v-card-title>{{faq.question}}</v-card-title>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn icon @click="show = !show">
              <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
            </v-btn>
          </v-card-actions>
          <v-expand-transition>
            <div v-show="show">
              <v-divider></v-divider>
              <v-card-text>{{faq.answer}}</v-card-text>
            </div>
          </v-expand-transition>
        </v-card>
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
      `http://covid19-news.herokuapp.com/api/covid19/faqs`
    );
    console.log(data);
    return { faqs: data.data };
  }
};
</script>