<template>
  <div id="app">
    <br />
    <p>
      <canvas id="graph" width="400" height="200"></canvas>
    </p>
  </div>
</template>

<script>
import Chart from "chart.js/dist/chart";

export default {
  props: {
    Cases: [],
    Death: [],
    Recovered: [],
  },
  mounted() {
    var ctx = document.getElementById("graph").getContext("2d");
    var bar = new Chart(ctx, {
      type: "bar",
      data: {
        labels: ["2", "2", "3", "day"],
        datasets: [
          {
            label: "Covid - 19",
            data: [12, 45, 67, "number cases"],
          },
        ],
      },
    });
    console.log(bar);
  },
  data() {
    return {};
  },
};
</script>
