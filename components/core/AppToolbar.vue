<template>
  <v-toolbar id="core-toolbar" flat prominent style="background: #eee;">
    <div class="v-toolbar-title">
      <v-toolbar-title class="tertiary--text font-weight-light">
        <v-btn v-if="responsive" class="default v-btn--simple" dark icon @click.stop="onClickBtn">
          <v-icon>mdi-view-list</v-icon>
        </v-btn>
        {{ title }}
      </v-toolbar-title>
    </div>

    <v-spacer />
    <v-toolbar-items>
      <v-flex align-center layout py-2>
        <v-text-field
          v-if="responsiveInput"
          class="mr-4 mt-2 purple-input"
          label="Search..."
          hide-details
          color="purple"
        />
      </v-flex>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
import { mapActions, mapGetters } from "vuex";

export default {
  data: () => ({
    notifications: [
      "Mike, John responded to your email",
      "You have 5 new tasks",
      "You're now a friend with Andrew",
      "Another Notification",
      "Another One"
    ],
    title: "Dashboard",
    responsive: true,
    responsiveInput: true
  }),
  watch: {
    $route(val) {
      this.title = val.name;
    }
  },
  computed: {
    ...mapGetters({
      drawer: "app/getDrawer"
    })
  },
  methods: {
    ...mapActions({
      setUsername: "user/setUsername",
      setDrawer: "app/setDrawer"
    }),

    onClickBtn() {
      this.setDrawer(!this.drawer);
    },
    onClick() {
      // Do something
    },
    onResponsiveInverted() {
      if (window.innerWidth < 991) {
        this.responsive = true;
        this.responsiveInput = false;
      } else {
        this.responsive = false;
        this.responsiveInput = true;
      }
    },
    async logout() {
      await this.setUsername(null);
      this.$router.push({ path: "/" });
    }
  },
  mounted() {
    this.onResponsiveInverted();
    window.addEventListener("resize", this.onResponsiveInverted);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.onResponsiveInverted);
  }
};
</script>

<style>
#core-toolbar a {
  text-decoration: none;
}
</style>
