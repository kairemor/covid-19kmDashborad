<template>
  <v-app>
    <core-filter />

    <core-toolbar />

    <core-drawer />

    <core-view />
  </v-app>
</template>

<script>
import coreFilter from "~/components/core/AppFilter";
import coreToolbar from "~/components/core/AppToolbar";
import coreDrawer from "~/components/core/AppDrawer";
import coreView from "~/components/core/AppView";
// import Chatbot from "~/components/core/Chatbot";

export default {
  components: {
    coreFilter,
    coreToolbar,
    coreDrawer,
    coreView
  },
  head() {
    return {
      script: [
        {
          src:
            "https://axlewebtech.com/clients/chatbots/axlewebtech/scripts/webchat.js"
        }
      ],
      link: [
        {
          rel: "stylesheet",
          href:
            "https://axlewebtech.com/clients/chatbots/axlewebtech/scripts/chatbot.css"
        }
      ]
    };
  },
  mounted() {
    bot_Init(
      "",
      true,
      400,
      500,
      "https://axlewebtech.com/clients/chatbots/axlewebtech/fullpage/images/customer-service.ico",
      "https://axleweb.tech/chatbotx?project=coronakm"
    );
  }
};
</script>


<style lang="scss">
/* Remove in 1.2 */
.v-datatable thead th.column.sortable i {
  vertical-align: unset;
}
</style>
