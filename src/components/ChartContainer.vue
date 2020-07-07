<template>
  <div class="container">
    <h1>Individuals</h1>
    <div class="chartContainer">
      <div class="yWrapper">
        <ul>
          <template v-for="(item, key) in yDataArray">
            <li v-bind:key="key">{{ item }}</li>
          </template>
        </ul>
      </div>
      <LineChart v-if="loaded" :height="400" :chartdata="chartdata" />
      <div class="xWrapper">
        <ul>
          <template v-for="(item, key) in xDataArray">
            <li v-bind:key="key">{{ item }}</li>
          </template>
        </ul>
      </div>
    </div>

    <h1>Companies</h1>
    <div class="chartContainer">
      <div class="yWrapper">
        <ul>
          <template v-for="(item, key) in yDataArray">
            <li v-bind:key="key">{{ item }}</li>
          </template>
        </ul>
      </div>
      <LineChart v-if="loaded" :height="400" :chartdata="companiesdata" />
      <div class="xWrapper">
        <ul>
          <template v-for="(item, key) in xDataArray">
            <li v-bind:key="key">{{ item }}</li>
          </template>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import LineChart from "./LineChart.vue";
import axios from "@/plugins/axios";

export default {
  name: "ChartContainer",
  components: { LineChart },
  data: () => ({
    loaded: false,
    chartdata: null,
    companiesdata: null,
    yDataArray: null,
    xDataArray: null,
  }),
  methods: {
    yReversed() {
      const arr = this.chartdata.yData;
      this.yDataArray = arr.reverse();
    },
    async getIndividuals() {
      this.loaded = false;
      try {
        const response = await axios.get("http://localhost:3000/individual");
        this.chartdata = response.data[0];

        this.loaded = true;
        this.xDataArray = this.chartdata.xData;
      } catch (err) {
        console.log(err);
        this.loaded = false;
      }
    },
    async getCompanies() {
      this.loaded = false;
      try {
        const response = await axios.get("http://localhost:3000/companies");
        this.companiesdata = response.data[0];
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
    await this.yReversed();
  },
};
</script>

<style lang="scss" scoped>
.container {
  max-width: 80%;
  margin: 0 auto;
  h1 {
    color: #849fb4;
    font-weight: 500;
    font-size: 26px;
  }
  .chartContainer {
    position: relative;
    background-color: #050711;
    margin-bottom: 100px;
    &:nth-child(2) {
      margin-top: 50px;
    }
    &:nth-child(4) {
      margin-top: 50px;
    }

    .yWrapper {
      ul {
        list-style-type: none;
        font-size: 1rem;
        font-weight: 400;
        position: absolute;
        color: #849fb4;
        margin-block-start: 0;
        padding-inline-start: 0;
        li {
          margin-bottom: 50px;
        }
      }
    }
    .xWrapper {
      position: absolute;
      width: 100%;
      bottom: 0;
      ul {
        display: flex;
        list-style-type: none;
        font-size: 0.9rem;
        font-weight: 400;
        justify-content: space-between;
        margin-left: 5em;
        margin-right: 16em;
        color: #849fb4;
        margin-block-start: 0;
        padding-inline-start: 0;
      }
    }
  }
}
</style>
