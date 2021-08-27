<template>
  <div>
    <h1 class="text-center">Hello home page</h1>
    <h1 class="text-center">Test data : {{ getData }}</h1>
    <Table />
  </div>
</template>

<script>
import Table from "../components/Table";
// import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      getData: "",
    };
  },
  components: {
    Table,
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

<style scoped></style>
