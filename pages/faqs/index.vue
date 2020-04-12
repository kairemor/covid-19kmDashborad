<template>
  <v-container fluid grid-list-xl>
    <v-layout wrap>
      <v-flex sm12 xs12 md4 lg3 v-for="(faq, index) in faqs" :key="index">
        <v-card class="mx-auto">
          <v-card-title>{{faq.question}}</v-card-title>
          <v-card-actions>
            <v-btn text color="blue" small rounded v-on:click="show = !show">Reponse</v-btn>
          </v-card-actions>
          <v-expand-transition>
            <div v-show="show">
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
  },
  data() {
    return {
      show: true
    };
  }
};
</script>