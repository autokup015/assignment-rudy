<template>
  <div>
    <div class="maxW">
      <div>
        <v-row no-gutters class="justify-center text-center">
          <v-col cols="12" sm="6">
            <v-date-picker v-model="dates" multiple></v-date-picker>
            <v-btn color="error" @click="clear">Clear</v-btn>
          </v-col>
        </v-row>
      </div>
      <br />
      <div class="d-flex justify-center">
        <v-alert
          border="right"
          colored-border
          type="error"
          elevation="2"
          width="150"
          :value="alert"
        >
          No data
        </v-alert>
      </div>
      <Graph
        :Cases="getCases"
        :Death="getDeaths"
        :Recovered="getRecovered"
        :day="dates"
      />
      <Table
        :Cases="getCases"
        :Death="getDeaths"
        :Recovered="getRecovered"
        :day="dates"
        @toggle="toggle"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Graph from "../components/Graph";
import Table from "../components/Table";

import moment from "moment";

export default {
  name: "Home",
  data() {
    return {
      getCases: [],
      getDeaths: [],
      getRecovered: [],
      dates: [],
      menu: false,
      // ----
      alert: false,
    };
  },
  components: {
    Table,
    Graph,
  },
  created() {
    axios
      .get("https://disease.sh/v3/covid-19/historical/all")
      .then((result) => {
        // ---------------------
        let arrCases = [];
        for (const value in result.data.cases) {
          let ob = {
            day: moment(value).format("M/DD/YY"),
            cases: result.data.cases[value],
          };
          arrCases.push(ob);
        }

        this.getCases = arrCases;

        // ---------------------

        let arrDeath = [];
        for (const value in result.data.deaths) {
          let newObject = {
            day: moment(value).format("M/DD/YY"),
            deaths: result.data.deaths[value],
          };
          arrDeath.push(newObject);
        }

        this.getDeaths = arrDeath;

        // ---------------------

        let arrRecovered = [];
        for (const value in result.data.recovered) {
          let newObject = {
            day: moment(value).format("M/DD/YY"),
            recovered: result.data.recovered[value],
          };
          arrRecovered.push(newObject);
        }

        this.getRecovered = arrRecovered;
      });
  },
  methods: {
    clear() {
      this.dates = [];
      this.alert = false;
    },
    toggle(value) {
      this.alert = value;
    },
  },
};
</script>

<style scoped>
.maxW {
  max-width: 1000px;
  margin: auto;
}
</style>
