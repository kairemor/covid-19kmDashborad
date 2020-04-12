<template>
  <v-container fill-height fluid grid-list-xl>
    <v-layout wrap>
      <v-flex sm12 md12 lg12>
        <h3
          align="center"
          class="font-weight-light mx-auto light-shadow"
        >Les chiffres du Covid19 niveau continentale</h3>
      </v-flex>
      <v-flex md12 lg12>
        <material-card color="blue" title="Les donnees par continent">
          <v-data-table :headers="headers_continent" :items="items" hide-actions>
            <template slot="headerCell" slot-scope="{ header }">
              <span class="font-weight-light text-warning text--darken-3" v-text="header.text" />
            </template>
            <template slot="items" slot-scope="{ index, item }">
              <td>{{ item.continent }}</td>
              <td>{{ item.confirmed }}</td>
              <td class="text-xs-right">{{ item.death }}</td>
              <td class="text-xs-right">{{ item.recovery }}</td>
              <td class="text-xs-right">{{ item.active }}</td>
              <td class="text-xs-right">{{ item.death_rate | pourcentage}}</td>
              <td class="text-xs-right">{{ item.recovery_rate | pourcentage }}</td>
            </template>
          </v-data-table>
        </material-card>
      </v-flex>
      <v-flex sm12 md12 lg12>
        <h3
          align="center"
          class="font-weight-light mx-auto light-shadow"
        >Les pays les plus touches dans le monde</h3>
      </v-flex>
      <v-flex md12 lg12>
        <material-card class="card-tabs" color="green">
          <v-flex slot="header">
            <v-tabs v-model="tabs" color="transparent" slider-color="white">
              <span class="subheading font-weight-light mr-3" style="align-self: center">Selon:</span>
              <v-tab class="mr-3">
                <v-icon class="mr-2">mdi-account-plus</v-icon>Confirmes
              </v-tab>
              <v-tab class="mr-3">
                <v-icon class="mr-2">mdi-account-off</v-icon>Deces
              </v-tab>
              <!-- <v-tab>
                <v-icon class="mr-2">mdi-account-check</v-icon>Gueris
              </v-tab>-->
            </v-tabs>
          </v-flex>
          <v-tabs-items v-model="tabs">
            <v-tab-item :key="0">
              <v-data-table :headers="headers" :items="items_confirmed" hide-actions>
                <template slot="headerCell" slot-scope="{ header }">
                  <span class="font-weight-light text-warning text--darken-3" v-text="header.text" />
                </template>
                <template slot="items" slot-scope="{ index, item }">
                  <td>{{ item.country }}</td>
                  <td>{{ item.confirmed }}</td>
                  <td class="text-xs-right">{{ item.death }}</td>
                  <td class="text-xs-right">{{ item.recovery }}</td>
                  <td class="text-xs-right">{{ item.active }}</td>
                  <td class="text-xs-right">{{ item.death_rate }}</td>
                  <td class="text-xs-right">{{ item.recovery_rate }}</td>
                </template>
              </v-data-table>
            </v-tab-item>
            <v-tab-item :key="1">
              <v-data-table :headers="headers" :items="items_deaths" hide-actions>
                <template slot="headerCell" slot-scope="{ header }">
                  <span class="font-weight-light text-warning text--darken-3" v-text="header.text" />
                </template>
                <template slot="items" slot-scope="{ index, item }">
                  <td>{{ item.country }}</td>
                  <td>{{ item.confirmed }}</td>
                  <td class="text-xs-right">{{ item.death }}</td>
                  <td class="text-xs-right">{{ item.recovery }}</td>
                  <td class="text-xs-right">{{ item.active }}</td>
                  <td class="text-xs-right">{{ item.death_rate }}</td>
                  <td class="text-xs-right">{{ item.recovery_rate }}</td>
                </template>
              </v-data-table>
            </v-tab-item>
            <!-- <v-tab-item :key="2">
              <v-data-table :headers="headers" :items="items_recovered" hide-actions>
                <template slot="headerCell" slot-scope="{ header }">
                  <span class="font-weight-light text-warning text--darken-3" v-text="header.text" />
                </template>
                <template slot="items" slot-scope="{ index, item }">
                  <td>{{ item.country }}</td>
                  <td>{{ item.confirmed }}</td>
                  <td class="text-xs-right">{{ item.death }}</td>
                  <td class="text-xs-right">{{ item.recovery }}</td>
                  <td class="text-xs-right">{{ item.active }}</td>
                </template>
              </v-data-table>
            </v-tab-item>-->
          </v-tabs-items>
        </material-card>
      </v-flex>

      <v-flex sm12 md12 lg12>
        <h3
          align="center"
          class="font-weight-light mx-auto light-shadow"
        >Les pays les plus touches en Afrique</h3>
      </v-flex>
      <v-flex md12 lg12>
        <material-card class="card-tabs" color="green">
          <v-flex slot="header">
            <v-tabs v-model="tabs" color="transparent" slider-color="white">
              <span class="subheading font-weight-light mr-3" style="align-self: center">Selon:</span>
              <v-tab class="mr-3">
                <v-icon class="mr-2">mdi-account-plus</v-icon>Confirmes
              </v-tab>
              <v-tab class="mr-3">
                <v-icon class="mr-2">mdi-account-off</v-icon>Deces
              </v-tab>
              <!-- <v-tab>
                <v-icon class="mr-2">mdi-account-check</v-icon>Gueris
              </v-tab>-->
            </v-tabs>
          </v-flex>
          <v-tabs-items v-model="tabs">
            <v-tab-item :key="0">
              <v-data-table :headers="headers" :items="items_africa_confirmed" hide-actions>
                <template slot="headerCell" slot-scope="{ header }">
                  <span class="font-weight-light text-warning text--darken-3" v-text="header.text" />
                </template>
                <template slot="items" slot-scope="{ index, item }">
                  <td>{{ item.country }}</td>
                  <td>{{ item.confirmed }}</td>
                  <td class="text-xs-right">{{ item.death }}</td>
                  <td class="text-xs-right">{{ item.recovery }}</td>
                  <td class="text-xs-right">{{ item.active }}</td>
                  <td class="text-xs-right">{{ item.death_rate | pourcentage}}</td>
                  <td class="text-xs-right">{{ item.recovery_rate | pourcentage}}</td>
                </template>
              </v-data-table>
            </v-tab-item>
            <v-tab-item :key="1">
              <v-data-table :headers="headers" :items="items_africa_deaths" hide-actions>
                <template slot="headerCell" slot-scope="{ header }">
                  <span class="font-weight-light text-warning text--darken-3" v-text="header.text" />
                </template>
                <template slot="items" slot-scope="{ index, item }">
                  <td>{{ item.country }}</td>
                  <td>{{ item.confirmed }}</td>
                  <td class="text-xs-right">{{ item.death }}</td>
                  <td class="text-xs-right">{{ item.recovery }}</td>
                  <td class="text-xs-right">{{ item.active }}</td>
                  <td class="text-xs-right">{{ item.death_rate }}</td>
                  <td class="text-xs-right">{{ item.recovery_rate }}</td>
                </template>
              </v-data-table>
            </v-tab-item>
            <!-- <v-tab-item :key="2">
              <v-data-table :headers="headers" :items="items_recovered" hide-actions>
                <template slot="headerCell" slot-scope="{ header }">
                  <span class="font-weight-light text-warning text--darken-3" v-text="header.text" />
                </template>
                <template slot="items" slot-scope="{ index, item }">
                  <td>{{ item.country }}</td>
                  <td>{{ item.confirmed }}</td>
                  <td class="text-xs-right">{{ item.death }}</td>
                  <td class="text-xs-right">{{ item.recovery }}</td>
                  <td class="text-xs-right">{{ item.active }}</td>
                </template>
              </v-data-table>
            </v-tab-item>-->
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
  // middleware: "authentication",
  components: {
    materialCard,
    materialChartCard,
    materialStatsCard
  },
  async asyncData() {
    const continentale_data = await axios.get(
      "https://coronakm.appspot.com/continent/"
    );
    const confirmed_mondiale = await axios.get(
      "https://coronakm.appspot.com/country/most-confirmed/10"
    );
    const deaths_mondiale = await axios.get(
      "https://coronakm.appspot.com/country/most-death/10"
    );

    console.log(confirmed_mondiale);

    return {
      headers_continent: [
        {
          sortable: false,
          text: "Continent",
          value: "continent"
        },
        {
          sortable: false,
          text: "Cas Confirmes",
          value: "confirmed"
        },
        {
          sortable: false,
          text: "Deces",
          value: "death",
          align: "right"
        },
        {
          sortable: false,
          text: "Gueris",
          value: "recovery",
          align: "right"
        },
        {
          sortable: false,
          text: "Sous traitement",
          value: "active",
          align: "right"
        },
        {
          sortable: false,
          text: "Taux mortalite",
          value: "death_rate",
          align: "center"
        },
        {
          sortable: false,
          text: "Taux de guerison",
          value: "recovery_rate",
          align: "center"
        }
      ],
      headers: [
        {
          sortable: false,
          text: "Pays",
          value: "country"
        },
        {
          sortable: false,
          text: "Cas Confirmes",
          value: "confirmed"
        },
        {
          sortable: false,
          text: "Deces",
          value: "death",
          align: "center"
        },
        {
          sortable: false,
          text: "Gueris",
          value: "recovery",
          align: "center"
        },
        {
          sortable: false,
          text: "Sous traitement",
          value: "active",
          align: "center"
        },
        {
          sortable: false,
          text: "Taux mortalite",
          value: "death_rate",
          align: "center"
        },
        {
          sortable: false,
          text: "Taux de guerison",
          value: "recovery_rate",
          align: "center"
        }
      ],
      items: continentale_data.data || [],
      items_recovered: confirmed_mondiale.data || [],
      items_confirmed: deaths_mondiale.data || [],
      items_deaths: deaths_mondiale.data || [],
      tabs: 0,
      list: {
        0: false,
        1: false,
        2: false
      }
    };
  },
  data() {
    return {
      // items_africa_recovered: confirmed_mondiale.data || [],
      items_africa_confirmed: [],
      items_africa_deaths: []
    };
  },
  head() {
    return {
      title: "Covid19 Statistique"
    };
  },
  methods: {
    complete(index) {
      this.list[index] = !this.list[index];
    }
  },
  async created() {
    const confirmed_africa = await axios.get(
      "https://coronakm.appspot.com/country/most-confirmed/10/Africa"
    );
    const deaths_africa = await axios.get(
      "https://coronakm.appspot.com/country/most-death/10/Africa"
    );

    // this.items = continentale_data.data;
    this.items_africa_confirmed = confirmed_africa.data;
    this.items_africa_deaths = deaths_africa.data;
    // this.items_recovered = deaths_mondiale.data;
    // console.log(this.items_confirmed);
  },
  filters: {
    pourcentage: function(name) {
      return (100 * name).toString().slice(0, 4) + "%";
    }
  }
};
</script>
<style scoped>
</style>