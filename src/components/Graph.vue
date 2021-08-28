<template>
  <div class="app">
    <apexchart width="1000" type="bar" :options="chartOptions" :series="series">
    </apexchart>
  </div>
</template>

<script>
import moment from "moment";

export default {
  props: {
    Cases: [],
    Death: [],
    Recovered: [],
    day: [],
  },
  data() {
    return {
      test1: [10, 20, 30],
      chartOptions: {
        chart: {
          id: "vuechart-example",
        },
        xaxis: {
          categories: [10, 20, 30, 40, 50],
        },
        dataLabels: {
          enabled: false,
        },
      },
      series: [
        {
          name: "Cases",
          data: [1, 2, 3, 4, 5],
        },
        {
          name: "Deaths",
          data: [1, 2, 3, 4, 5],
        },
        {
          name: "Recovered",
          data: [1, 2, 3, 4, 5],
        },
      ],
    };
  },

  watch: {
    day() {
      if (this.day.length == 0) {
        this.defaultData();
      } else {
        this.setData();
      }
    },
    Cases() {
      this.defaultData();
    },
  },
  methods: {
    setData() {
      //
      // Filter Cases and day
      //

      let cloneCases = [...this.Cases];
      let arrCases = cloneCases.filter((data) => {
        for (let i = 0; i < this.day.length; i++) {
          const ele = moment(this.day[i]).format("M/DD/YY");
          if (data.day == ele) {
            return data;
          }
        }
      });

      let finalCases = [];
      let finalDay = [];

      arrCases.forEach((data) => {
        finalCases.push(data.cases);
        finalDay.push(data.day);
      });

      //
      // Filter Deaths
      //

      let cloneDeath = [...this.Death];
      let arrDeath = cloneDeath.filter((data) => {
        for (let i = 0; i < this.day.length; i++) {
          const ele = moment(this.day[i]).format("M/DD/YY");
          if (data.day == ele) {
            return data;
          }
        }
      });
      let finalDeath = [];

      arrDeath.forEach((data) => {
        finalDeath.push(data.deaths);
      });

      //
      // Filter Recovered
      //

      let cloneRecovered = [...this.Recovered];
      let arrRecovered = cloneRecovered.filter((data) => {
        for (let i = 0; i < this.day.length; i++) {
          const ele = moment(this.day[i]).format("M/DD/YY");
          if (data.day == ele) {
            return data;
          }
        }
      });
      let finalRecovered = [];

      arrRecovered.forEach((data) => {
        finalRecovered.push(data.recovered);
      });

      //
      //  Set value to Chart
      //

      (this.chartOptions = {
        chart: {
          id: "vuechart-example",
        },
        xaxis: {
          categories: finalDay,
        },
      }),
        (this.series = [
          {
            name: "Cases",
            data: finalCases,
          },
          {
            name: "Deaths",
            data: finalDeath,
          },
          {
            name: "Recovered",
            data: finalRecovered,
          },
        ]);
    },
    defaultData() {
      //
      // Set default data only
      //
      let defaultDay = this.Cases.map((data) => {
        return data.day;
      });

      let defaultCases = this.Cases.map((data) => {
        return data.cases;
      });

      let defaultDeath = this.Death.map((data) => {
        return data.deaths;
      });

      let defaultRecovered = this.Recovered.map((data) => {
        return data.recovered;
      });

      //
      // Set value default
      //

      (this.chartOptions = {
        chart: {
          id: "vuechart-example",
        },
        xaxis: {
          categories: defaultDay,
        },
      }),
        (this.series = [
          {
            name: "Cases",
            data: defaultCases,
          },
          {
            name: "Deaths",
            data: defaultDeath,
          },
          {
            name: "Recovered",
            data: defaultRecovered,
          },
        ]);
    },
  },
};
</script>
