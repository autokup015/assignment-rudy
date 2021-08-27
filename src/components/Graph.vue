<template>
  <div id="app">
    <p>
      <canvas id="graph" width="400" height="200"></canvas>
    </p>
  </div>
</template>

<script>
import Chart from "chart.js/dist/chart";

export default {
  mounted() {
    var ctx = document.getElementById("graph").getContext("2d");
    var bar = new Chart(ctx, {
      type: "line",
      data: {
        labels: ["1", "2", "3"],
        datasets: [
          {
            label: "# of Vote",
            data: [12, 45, 67],
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
