<template>
  <v-container fill-height fluid grid-list-xl>
    <v-layout wrap>
      <v-flex sm12 md12 lg12>
        <h2 align="center" class="font-weight-light mx-auto light-shadow">Senegal</h2>
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="blue"
          icon="mdi-store"
          title="Cas confirmes"
          v-bind:value="senegal_data.confirmed"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="red"
          icon="mdi-content-copy"
          title="Deces"
          v-bind:value="senegal_data.deaths"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="green"
          icon="mdi-information-outline"
          title="Gueris"
          v-bind:value="senegal_data.recovered"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="orange"
          icon="mdi-twitter"
          title="Actif"
          v-bind:value="senegal_data.active"
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
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="blue"
          icon="mdi-store"
          title="Cas confirmes"
          v-bind:value="all_data.confirmed"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="red"
          icon="mdi-content-copy"
          title="Deces"
          v-bind:value="all_data.death"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="green"
          icon="mdi-information-outline"
          title="Gueris"
          v-bind:value="all_data.recovery"
        />
      </v-flex>
      <v-flex sm6 xs12 md6 lg3>
        <material-stats-card
          color="orange"
          icon="mdi-twitter"
          title="Actif"
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

      <v-flex md12 lg6>
        <material-card
          color="orange"
          title="Employee Stats"
          text="New employees on 15th September, 2016"
        >
          <v-data-table :headers="headers" :items="items" hide-actions>
            <template slot="headerCell" slot-scope="{ header }">
              <span class="font-weight-light text-warning text--darken-3" v-text="header.text" />
            </template>
            <template slot="items" slot-scope="{ index, item }">
              <td>{{ index + 1 }}</td>
              <td>{{ item.name }}</td>
              <td class="text-xs-right">{{ item.salary }}</td>
              <td class="text-xs-right">{{ item.country }}</td>
              <td class="text-xs-right">{{ item.city }}</td>
            </template>
          </v-data-table>
        </material-card>
      </v-flex>
      <v-flex md12 lg6>
        <material-card class="card-tabs" color="green">
          <v-flex slot="header">
            <v-tabs v-model="tabs" color="transparent" slider-color="white">
              <span class="subheading font-weight-light mr-3" style="align-self: center">Tasks:</span>
              <v-tab class="mr-3">
                <v-icon class="mr-2">mdi-bug</v-icon>Bugs
              </v-tab>
              <v-tab class="mr-3">
                <v-icon class="mr-2">mdi-code-tags</v-icon>Website
              </v-tab>
              <v-tab>
                <v-icon class="mr-2">mdi-cloud</v-icon>Server
              </v-tab>
            </v-tabs>
          </v-flex>

          <v-tabs-items v-model="tabs">
            <v-tab-item v-for="n in 3" :key="n">
              <v-list three-line>
                <v-list-tile @click="complete(0)">
                  <v-list-tile-action>
                    <v-checkbox :value="list[0]" color="green" />
                  </v-list-tile-action>
                  <v-list-tile-title>Sign contract for "What are conference organized afraid of?"</v-list-tile-title>
                  <div class="d-flex">
                    <v-tooltip top content-class="top">
                      <v-btn slot="activator" class="v-btn--simple" color="success" icon>
                        <v-icon color="primary">mdi-pencil</v-icon>
                      </v-btn>
                      <span>Edit</span>
                    </v-tooltip>
                    <v-tooltip top content-class="top">
                      <v-btn slot="activator" class="v-btn--simple" color="danger" icon>
                        <v-icon color="error">mdi-close</v-icon>
                      </v-btn>
                      <span>Close</span>
                    </v-tooltip>
                  </div>
                </v-list-tile>
                <v-divider />
                <v-list-tile @click="complete(1)">
                  <v-list-tile-action>
                    <v-checkbox :value="list[1]" color="success" />
                  </v-list-tile-action>
                  <v-list-tile-title>Lines From Great Russian Literature? Or E-mails From My Boss?</v-list-tile-title>
                  <div class="d-flex">
                    <v-tooltip top content-class="top">
                      <v-btn slot="activator" class="v-btn--simple" color="success" icon>
                        <v-icon color="primary">mdi-pencil</v-icon>
                      </v-btn>
                      <span>Edit</span>
                    </v-tooltip>

                    <v-tooltip top content-class="top">
                      <v-btn slot="activator" class="v-btn--simple" color="danger" icon>
                        <v-icon color="error">mdi-close</v-icon>
                      </v-btn>
                      <span>Close</span>
                    </v-tooltip>
                  </div>
                </v-list-tile>
                <v-divider />
                <v-list-tile @click="complete(2)">
                  <v-list-tile-action>
                    <v-checkbox :value="list[2]" color="success" />
                  </v-list-tile-action>
                  <v-list-tile-title>Flooded: One year later, assessing what was lost and what was found when a ravaging rain swept through metro Detroit</v-list-tile-title>
                  <div class="d-flex">
                    <v-tooltip top content-class="top">
                      <v-btn slot="activator" class="v-btn--simple" color="success" icon>
                        <v-icon color="primary">mdi-pencil</v-icon>
                      </v-btn>
                      <span>Edit</span>
                    </v-tooltip>
                    <v-tooltip top content-class="top">
                      <v-btn slot="activator" class="v-btn--simple" color="danger" icon>
                        <v-icon color="error">mdi-close</v-icon>
                      </v-btn>
                      <span>Close</span>
                    </v-tooltip>
                  </div>
                </v-list-tile>
              </v-list>
            </v-tab-item>
          </v-tabs-items>
        </material-card>
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
  middleware: "authentication",
  components: {
    materialCard,
    materialChartCard,
    materialStatsCard
  },
  data() {
    return {
      all_data: {},
      senegal_data: {},
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
      },
      headers: [
        {
          sortable: false,
          text: "ID",
          value: "id"
        },
        {
          sortable: false,
          text: "Name",
          value: "name"
        },
        {
          sortable: false,
          text: "Salary",
          value: "salary",
          align: "right"
        },
        {
          sortable: false,
          text: "Country",
          value: "country",
          align: "right"
        },
        {
          sortable: false,
          text: "City",
          value: "city",
          align: "right"
        }
      ],
      items: [
        {
          name: "Dakota Rice",
          country: "Niger",
          city: "Oud-Tunrhout",
          salary: "$35,738"
        },
        {
          name: "Minerva Hooper",
          country: "Curaçao",
          city: "Sinaai-Waas",
          salary: "$23,738"
        },
        {
          name: "Sage Rodriguez",
          country: "Netherlands",
          city: "Overland Park",
          salary: "$56,142"
        },
        {
          name: "Philip Chanley",
          country: "Korea, South",
          city: "Gloucester",
          salary: "$38,735"
        },
        {
          name: "Doris Greene",
          country: "Malawi",
          city: "Feldkirchen in Kārnten",
          salary: "$63,542"
        }
      ],
      tabs: 0,
      list: {
        0: false,
        1: false,
        2: false
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
    const alldata = await axios.get(
      "https://aiobackend.herokuapp.com/data/all"
    );
    const senegaldata = await axios.get(
      "https://aiobackend.herokuapp.com/country_data/country"
    );
    const all_graph_data = await axios.get(
      "https://coronakm.appspot.com/grapth_data/"
    );

    const country_graph_data = await axios.get(
      "https://coronakm.appspot.com/grapth_data/Senegal"
    );

    this.all_data = alldata.data;
    this.senegal_data = senegaldata.data;

    const values_confirmed = all_graph_data.data.values_confirmed
      .split(",")
      .map(value => parseInt(value));
    const values_recovered = all_graph_data.data.values_recovered
      .split(",")
      .map(value => parseInt(value));
    const values_deaths = all_graph_data.data.values_deaths
      .split(",")
      .map(value => parseInt(value));

    const country_values_confirmed = country_graph_data.data.values_confirmed
      .split(",")
      .map(value => parseInt(value));
    const country_values_recovered = country_graph_data.data.values_recovered
      .split(",")
      .map(value => parseInt(value));
    const country_values_deaths = country_graph_data.data.values_deaths
      .split(",")
      .map(value => parseInt(value));

    const column_name = all_graph_data.data.columns.split(",");
    this.confirmedCasesChart.data.labels = column_name;
    this.recoveredCasesChart.data.labels = column_name;
    this.deathsCasesChart.data.labels = column_name;

    this.countryConfirmedCasesChart.data.labels = column_name;
    this.countryRecoveredCasesChart.data.labels = column_name;
    this.countryDeathsCasesChart.data.labels = column_name;

    this.confirmedCasesChart.data.series.push(values_confirmed);
    this.recoveredCasesChart.data.series.push(values_recovered);
    this.deathsCasesChart.data.series.push(values_deaths);

    this.countryConfirmedCasesChart.data.series.push(country_values_confirmed);
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
