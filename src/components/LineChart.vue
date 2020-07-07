<script>
import { Line } from "vue-chartjs";

export default {
  extends: Line,
  props: ["chartdata", "height"],
  data: () => ({
    gradient: null,
    options: {
      legend: {
        display: false,
      },
      title: {
        text: "Monthly Stock Prices",
        x: "center",
        textStyle: {
          fontSize: 24,
        },
      },
      color: ["#127ac2"],
      scales: {
        yAxes: [
          {
            display: true,
            position: "left",
            ticks: {
              display: false,
              beginAtZero: false,
              max: 16,
              min: 0,
              stepSize: 3,
              fontColor: "#849fb4",
              fontFamily: "Montserrat",
              fontSize: 14,
            },
          },
        ],
        xAxes: [
          {
            display: false,
            ticks: {
              beginAtZero: false,
              fontColor: "#849fb4",
              fontFamily: "Montserrat",
              fontSize: 14,
              marginLeft: 24,
            },
          },
        ],
      },
      responsive: true,
      maintainAspectRatio: false,
    },
  }),
  computed: {
    fillGrad() {
      return "linear-gradient(90deg, rgb(78, 255, 207) 0%, rgb(8, 164, 188) 100%)";
    },
  },
  methods: {
    gradCreate() {
      if (this.chartdata.datasets[0].label === "Individual") {
        this.gradient = this.$refs.canvas
          .getContext("2d")
          .createLinearGradient(0, 0, 0, 450);

        this.gradient.addColorStop(0, "rgb(78, 255, 207, 100)");
        this.gradient.addColorStop(0.5, "rgb(44, 102, 121, 100)");
        this.gradient.addColorStop(0.8, "rgb(29, 53, 80, 100)");
        this.gradient.addColorStop(1, "rgb(12, 16, 29, 20)");
      } else {
        this.gradient = this.$refs.canvas
          .getContext("2d")
          .createLinearGradient(0, 0, 0, 450);

        this.gradient.addColorStop(0, "rgb(255, 86, 238)");
        this.gradient.addColorStop(1, "rgb(62, 87, 194, 0)");
      }
    },
  },
  mounted() {
    this.gradCreate();

    this.renderChart(
      {
        labels: this.chartdata.labels,
        datasets: [
          {
            label: false,
            defaultFontColor: "black",
            backgroundColor: this.gradient,
            data: this.chartdata.datasets[0].data,
            pointBackgroundColor: "transparent",
          },
        ],
      },
      this.options
    );
  },
};
</script>
