<script>
import { Line } from "vue-chartjs";

export default {
  extends: Line,
  props: ["chartdata"],
  data: () => ({
    gradient: null,
    options: {
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
      if (this.chartdata[0].datasets[0].label === 'Individual') {
        this.gradient = this.$refs.canvas
        .getContext("2d")
        .createLinearGradient(0, 0, 0, 450);

      this.gradient.addColorStop(0, "rgb(78, 255, 207)");
      this.gradient.addColorStop(1, "rgb(8, 164, 188)");
      } else {
        this.gradient = this.$refs.canvas
        .getContext("2d")
        .createLinearGradient(0, 0, 0, 450);

      this.gradient.addColorStop(0, "rgb(255, 86, 238)");
      this.gradient.addColorStop(1, "rgb(62, 87, 194)");
      }
      
    },
  },
  mounted() {
    this.gradCreate();

    this.renderChart(
      {
        labels: this.chartdata[0].labels,
        datasets: [
          {
            label: '',
            backgroundColor: this.gradient,
            data: this.chartdata[0].datasets[0].data,
          },
        ],
      },
      {
        responsive: true,
        title: {
            display: false
        }
      }
    );
  },
};
</script>

<style></style>
