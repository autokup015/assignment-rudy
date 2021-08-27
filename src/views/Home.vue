<template>
  <div>
    <h1 class="text-center">Hello home page</h1>
    <div class="maxW">
      <Graph />
      <Table />
    </div>
  </div>
</template>

<script>
// import axios from "axios";
import Graph from "../components/Graph";
import Table from "../components/Table";

export default {
  name: "Home",
  data() {
    return {
      getData: "",
    };
  },
  components: {
    Table,
    Graph,
  },
  // created() {
  //   axios
  //     .get("https://disease.sh/v3/covid-19/historical/all")
  //     .then((result) => {
  //       this.getData = result.data;
  //     });
  // },
};
</script>

<style scoped>
.maxW {
  max-width: 1000px;
  margin: auto;
}
</style>
