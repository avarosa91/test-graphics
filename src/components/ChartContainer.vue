<template>
  <div class="container">
    <h1>Individuals</h1>
    <div class="chartContainer">
      <LineChart v-if="loaded" :chartdata="chartdata" />
    </div>

    <h1>Companies</h1>
    <div class="chartContainer">
      <LineChart v-if="loaded" :chartdata="companiesdata" />
    </div>
  </div>
</template>

<script>
import LineChart from "./LineChart.vue";
import axios from "@/plugins/axios";

export default {
  name: "LineChartContainer",
  components: { LineChart },
  data: () => ({
    loaded: false,
    chartdata: null,
    companiesdata: null,
  }),
  methods: {
    async getIndividuals() {
      this.loaded = false;
      try {
        const response = await axios.get("http://localhost:3000/individual");
        console.log(response.data);
        this.chartdata = response.data;
        this.loaded = true;
      } catch (err) {
        console.log(err);
        this.loaded = false;
      }
    },
    async getCompanies() {
      this.loaded = false;
      try {
        const response = await axios.get("http://localhost:3000/companies");
        console.log(response.data);
        this.companiesdata = response.data;
        this.loaded = true;
      } catch (err) {
        console.log(err);
        this.loaded = false;
      }
    },
  },
  async mounted() {
    await this.getIndividuals();
    await this.getCompanies();
  },
};
</script>

<style lang="scss">
.container {
}
</style>
