<!-- https://github.com/ehajri/vue-chartjs-financial/blob/master/src/views/Candlestick.vue -->
<template>
  <div class="small">
    <Candlestick
      :chart-data="datacollection"
      :options="options"
    />
  </div>
</template>

<script>
import Candlestick from "@/components/Candlestick.js";
export default {
  components: {
    Candlestick
  },
  data() {
    return {
      datacollection: {},
      options: {}
    };
  },
  mounted() {
    this.fillData();
  },
  methods: {
    fillData() {
      this.datacollection = {
        datasets: [
          {
            label: "OHLC",
            data: this.generateRandomData()
          }
        ]
      };
    },
    generateRandomData(initial = 1000, count = 10, changeRange = 100) {
      let o = initial,
        h,
        l,
        c,
        t = new Date("2020-01-01").getTime();
      return [...Array(count)].map((_, i) => {
        o = c || o;
        h = o + this.randomChange(changeRange) / 2;
        l = o - this.randomChange(changeRange) / 2;
        c = o + (this.randomChange(changeRange) - changeRange / 2);
        t += 24 * 60 * 60 * 1000;
        return {
          o,
          h,
          l,
          c,
          t
        };
      });
    },
    randomChange(range = 100) {
      return Math.random() * range;
    }
  }
};
</script>