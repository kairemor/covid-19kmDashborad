<template>
  <v-container fill-height fluid grid-list-xl>
    <v-layout wrap>
      <v-flex sm12 md12 lg12>
        <h2 align="center" class="font-weight-light mx-auto light-shadow">Senegal</h2>
        <p align="center" class="font-weight-light mx-auto light-shadow">
          Taux de mortalite :
          <b>{{ ((senegal_data.death_rate * 100).toString()).slice(0,4) + "%" }}</b>
        </p>
        <p align="center" class="font-weight-light mx-auto light-shadow">
          Taux de guerison :
          <b>{{ ((senegal_data.recovery_rate * 100).toString()).slice(0,4) + "%" }}</b>
        </p>
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="blue"
          icon="mdi-account-plus"
          title="Cas confirmes"
          v-bind:value="senegal_data.confirmed.toString()"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="red"
          icon="mdi-account-off"
          title="Deces"
          v-bind:value="senegal_data.deaths.toString()"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="green"
          icon="mdi-account-check"
          title="Gueris"
          v-bind:value="senegal_data.recovered.toString()"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="orange"
          icon="mdi-account-star"
          title="Sous traitement"
          v-bind:value="senegal_data.active.toString()"
        />
      </v-flex>

      <v-flex md12 sm12 lg4>
        <material-chart-card
          :data="countryConfirmedCasesChart.data"
          :options="countryConfirmedCasesChart.options"
          color="info"
          type="Line"
        >
          <h4 class="title font-weight-light">Cas Confirmes</h4>
        </material-chart-card>
      </v-flex>
      <v-flex md12 sm12 lg4>
        <material-chart-card
          :data="countryRecoveredCasesChart.data"
          :options="countryRecoveredCasesChart.options"
          color="green"
          type="Line"
        >
          <h4 class="title font-weight-light">Gueris</h4>
        </material-chart-card>
      </v-flex>
      <v-flex md12 sm12 lg4>
        <material-chart-card
          :data="countryDeathsCasesChart.data"
          :options="countryDeathsCasesChart.options"
          color="red"
          type="Line"
        >
          <h4 class="title font-weight-light">Deces</h4>
        </material-chart-card>
      </v-flex>

      <v-flex sm12 md12 lg12>
        <h2 align="center" class="font-weight-light mx-auto light-shadow">Mondiale</h2>
        <p align="center" class="font-weight-light mx-auto light-shadow">
          Taux de mortalite :
          <b>{{ ((all_data.death_rate * 100).toString()).slice(0,4) + "%" }}</b>
        </p>
        <p align="center" class="font-weight-light mx-auto light-shadow">
          Taux de guerison :
          <b>{{ ((all_data.recovery_rate * 100).toString()).slice(0,4) + "%" }}</b>
        </p>
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="blue"
          icon="mdi-account-plus"
          title="Cas confirmes"
          v-bind:value="all_data.confirmed"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="red"
          icon="mdi-account-off"
          title="Deces"
          v-bind:value="all_data.death"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="green"
          icon="mdi-account-check"
          title="Gueris"
          v-bind:value="all_data.recovery"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="orange"
          icon="mdi-account-star"
          title="Sous traitement"
          v-bind:value="all_data.active"
        />
      </v-flex>

      <v-flex md12 sm12 lg4>
        <material-chart-card
          :data="confirmedCasesChart.data"
          :options="confirmedCasesChart.options"
          color="info"
          type="Line"
        >
          <h4 class="title font-weight-light">Cas Confirmes</h4>
        </material-chart-card>
      </v-flex>
      <v-flex md12 sm12 lg4>
        <material-chart-card
          :data="recoveredCasesChart.data"
          :options="recoveredCasesChart.options"
          color="green"
          type="Line"
        >
          <h4 class="title font-weight-light">Gueris</h4>
        </material-chart-card>
      </v-flex>
      <v-flex md12 sm12 lg4>
        <material-chart-card
          :data="deathsCasesChart.data"
          :options="deathsCasesChart.options"
          color="red"
          type="Line"
        >
          <h4 class="title font-weight-light">Deces</h4>
        </material-chart-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import materialCard from "~/components/material/AppCard";
import materialChartCard from "~/components/material/AppChartCard";
import materialStatsCard from "~/components/material/AppStatsCard";
import axios from "axios";
export default {
  layout: "dashboard",
  // middleware: "authentication",
  components: {
    materialCard,
    materialChartCard,
    materialStatsCard
  },
  async asyncData() {
    const { data } = await axios.get(
      `https://aiobackend.herokuapp.com/country_data/country_name/`
    );

    const alldata = await axios.get(
      "https://aiobackend.herokuapp.com/data/all"
    );
    // const all_graph_data = await axios.get(
    //   "https://coronakm.appspot.com/grapth_data/"
    // );

    // const country_graph_data = await axios.get(
    //   "https://coronakm.appspot.com/grapth_data/Senegal"
    // );

    // this.all_data = alldata.data;
    // this.senegal_data = senegaldata.data;

    // const values_confirmed = all_graph_data.data.values_confirmed
    //   .split(",")
    //   .map(value => parseInt(value));
    // const values_recovered = all_graph_data.data.values_recovered
    //   .split(",")
    //   .map(value => parseInt(value));
    // const values_deaths = all_graph_data.data.values_deaths
    //   .split(",")
    //   .map(value => parseInt(value));

    // const country_values_confirmed = country_graph_data.data.values_confirmed
    //   .split(",")
    //   .map(value => parseInt(value));
    // const country_values_recovered = country_graph_data.data.values_recovered
    //   .split(",")
    //   .map(value => parseInt(value));
    // const country_values_deaths = country_graph_data.data.values_deaths
    //   .split(",")
    //   .map(value => parseInt(value));

    // const column_name = all_graph_data.data.columns.split(",");

    return {
      senegal_data: data,
      all_data: alldata.data
      // confirmedCasesChart: {
      //   data: {
      //     labels: column_name,
      //     series: values_confirmed
      //   },
      //   options: {
      //     low: 0,
      //     high: values_confirmed[values_confirmed.length - 1], // creative tim: we recommend you to set the high sa the biggest value + something for a better look
      //     chartPadding: {
      //       top: 0,
      //       right: 0,
      //       bottom: 0,
      //       left: 10
      //     }
      //   }
      // },
      // recoveredCasesChart: {
      //   data: {
      //     labels: column_name,
      //     series: values_recovered
      //   },
      //   options: {
      //     low: 0,
      //     high: values_recovered[values_recovered.length - 1], // creative tim: we recommend you to set the high sa the biggest value + something for a better look
      //     chartPadding: {
      //       top: 0,
      //       right: 0,
      //       bottom: 0,
      //       left: 10
      //     }
      //   }
      // },
      // deathsCasesChart: {
      //   data: {
      //     labels: column_name,
      //     series: values_deaths
      //   },
      //   options: {
      //     low: 0,
      //     high: values_deaths[values_deaths.length - 1], // creative tim: we recommend you to set the high sa the biggest value + something for a better look
      //     chartPadding: {
      //       top: 0,
      //       right: 0,
      //       bottom: 0,
      //       left: 10
      //     }
      //   }
      // },
      // countryConfirmedCasesChart: {
      //   data: {
      //     labels: column_name,
      //     series: country_values_confirmed
      //   },
      //   options: {
      //     low: 0,
      //     high: country_values_confirmed[country_values_confirmed.length - 1], // creative tim: we recommend you to set the high sa the biggest value + something for a better look
      //     chartPadding: {
      //       top: 0,
      //       right: 0,
      //       bottom: 0,
      //       left: 10
      //     }
      //   }
      // },
      // countryRecoveredCasesChart: {
      //   data: {
      //     labels: column_name,
      //     series: country_values_recovered
      //   },
      //   options: {
      //     low: 0,
      //     high: country_values_recovered[country_values_recovered.length - 1], // creative tim: we recommend you to set the high sa the biggest value + something for a better look
      //     chartPadding: {
      //       top: 0,
      //       right: 0,
      //       bottom: 0,
      //       left: 10
      //     }
      //   }
      // },
      // countryDeathsCasesChart: {
      //   data: {
      //     labels: column_name,
      //     series: country_values_deaths
      //   },
      //   options: {
      //     low: 0,
      //     high: country_values_deaths[country_values_deaths.length - 1], // creative tim: we recommend you to set the high sa the biggest value + something for a better look
      //     chartPadding: {
      //       top: 0,
      //       right: 0,
      //       bottom: 0,
      //       left: 10
      //     }
      //   }
      // }
    };
  },
  data() {
    return {
      // all_data: {},
      // senegal_data: {},
      confirmedCasesChart: {
        data: {
          labels: [],
          series: []
        },
        options: {
          low: 0,
          high: 1000000, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 10
          }
        }
      },
      recoveredCasesChart: {
        data: {
          labels: [],
          series: []
        },
        options: {
          low: 0,
          high: 1000000, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 10
          }
        }
      },
      deathsCasesChart: {
        data: {
          labels: [],
          series: []
        },
        options: {
          low: 0,
          high: 1000000, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 10
          }
        }
      },
      countryConfirmedCasesChart: {
        data: {
          labels: [],
          series: []
        },
        options: {
          low: 0,
          high: 1000000, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 10
          }
        }
      },
      countryRecoveredCasesChart: {
        data: {
          labels: [],
          series: []
        },
        options: {
          low: 0,
          high: 1000000, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 10
          }
        }
      },
      countryDeathsCasesChart: {
        data: {
          labels: [],
          series: []
        },
        options: {
          low: 0,
          high: 1000000, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 10
          }
        }
      }
    };
  },
  methods: {
    complete(index) {
      this.list[index] = !this.list[index];
    }
  },
  mounted() {
    this.$nextTick(() => {
      /*this.dailySalesChart.options = {
          lineSmooth: this.$chartist.Interpolation.cardinal({
            tension: 0
          }),
          low: 0,
          high: 50, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 0
          }
        };
        this.dataCompletedTasksChart.options = {
          lineSmooth: this.$chartist.Interpolation.cardinal({
            tension: 0
          }),
          low: 0,
          high: 1000, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 0
          }
        };*/
    });
  },
  async created() {
    // const senegaldata = await axios.get(
    //   "https://aiobackend.herokuapp.com/country_data/country/148"
    // );
    const all_graph_data = await axios.get(
      "https://coronakm.appspot.com/grapth_data/"
    );

    const country_graph_data = await axios.get(
      "https://coronakm.appspot.com/grapth_data/Senegal"
    );

    // this.all_data = alldata.data;
    // this.senegal_data = senegaldata.data;

    const values_confirmed = all_graph_data.data.values_confirmed
      .split(",")
      .map(value => parseInt(value));
    const values_recovered = all_graph_data.data.values_recovered
      .split(",")
      .map(value => parseInt(value));
    const values_deaths = all_graph_data.data.values_deaths
      .split(",")
      .map(value => parseInt(value));

    const values_active = values_confirmed.map(
      (value, index) => value - values_recovered[index] - values_deaths[index]
    );

    const country_values_confirmed = country_graph_data.data.values_confirmed
      .split(",")
      .map(value => parseInt(value));
    const country_values_recovered = country_graph_data.data.values_recovered
      .split(",")
      .map(value => parseInt(value));
    const country_values_deaths = country_graph_data.data.values_deaths
      .split(",")
      .map(value => parseInt(value));

    const country_values_active = country_values_confirmed.map(
      (value, index) =>
        value - country_values_recovered[index] - country_values_deaths[index]
    );

    const column_name = all_graph_data.data.columns.split(",");
    this.confirmedCasesChart.data.labels = column_name;
    this.recoveredCasesChart.data.labels = column_name;
    this.deathsCasesChart.data.labels = column_name;

    this.countryConfirmedCasesChart.data.labels = column_name;
    this.countryRecoveredCasesChart.data.labels = column_name;
    this.countryDeathsCasesChart.data.labels = column_name;

    this.confirmedCasesChart.data.series.push(values_confirmed);
    this.confirmedCasesChart.data.series.push(values_active);
    this.recoveredCasesChart.data.series.push(values_recovered);
    this.deathsCasesChart.data.series.push(values_deaths);

    this.countryConfirmedCasesChart.data.series.push(country_values_confirmed);
    this.countryConfirmedCasesChart.data.series.push(country_values_active);
    this.countryRecoveredCasesChart.data.series.push(country_values_recovered);
    this.countryDeathsCasesChart.data.series.push(country_values_deaths);

    this.confirmedCasesChart.options.high =
      values_confirmed[values_confirmed.length - 1];
    this.recoveredCasesChart.options.high =
      values_recovered[values_recovered.length - 1];
    this.deathsCasesChart.options.high =
      values_deaths[values_deaths.length - 1];

    this.countryConfirmedCasesChart.options.high =
      country_values_confirmed[country_values_confirmed.length - 1];
    this.countryRecoveredCasesChart.options.high =
      country_values_recovered[country_values_recovered.length - 1];
    this.countryDeathsCasesChart.options.high =
      country_values_deaths[country_values_deaths.length - 1];
  }
};
</script>
<style lang="scss">
.shadowed {
  text-shadow: 5px 5px 3px #333;
}

.light-shadow {
  text-shadow: 0.2em 0.2em 0.2em rgba(0, 0, 0, 0.2);
}

.multiple-shadows {
  text-shadow: 5px 5px 5px rgba(0, 0, 0, 0.1), 10px 10px 10px rgba(0, 0, 0, 0.2);
}
</style>
