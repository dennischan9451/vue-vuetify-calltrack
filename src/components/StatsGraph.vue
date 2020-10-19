<template>
  <v-card class="mb-4">
    <v-card-text class="pa-0">
      <div class="d-flex justify-space-between px-3 pt-4">
        <div class="d-flex filter-options">
          <span class="subtitle-2 black--text font-weight-bold mr-2 mt-3">CALL STATS FOR: </span>
          <div class="d-inline-flex">
            <v-select
              v-model="statsFor"
              :item-text="'text'"
              :item-value="'value'"
              :items="StatsForItems"
              outlined
              dense
              class="subtitle-2"
            ></v-select>
          </div>
          <v-checkbox
            v-model="excludeRejCalls"
            label="Exclude Rejected Calls"
            dense
            class="subtitle-2 ml-3 mt-1"
          ></v-checkbox>
        </div>
        <div class="d-inline-flex">
          <v-select
            v-model="filterDate"
            :item-text="'text'"
            :item-value="'value'"
            :items="filterDates"
            solo
            dense
            class="subtitle-2"
          ></v-select>
        </div>
      </div>

      <div class="stats-graph pa-2">
        <line-chart v-if="dataCollection" :chartdata="dataCollection" :options="chartOptions"></line-chart>
      </div>
    </v-card-text>
  </v-card>
</template>

<script>
import LineChart from './LineChart.js'

const chartOptions = {
  responsive: true,
  maintainAspectRatio: false,
  scales: {
    yAxes: [{
      ticks: {
        min: 0,
        precision: 0,
        fontSize: 12
      }
    }],
    xAxes: [{
      ticks: {
        fontSize: 12
      },
      gridLines: {
        display: false
      }
    }]
  }
}

export default {
  components: {
    LineChart
  },
  data () {
    return {
      statsFor: 1,
      excludeRejCalls: true,
      StatsForItems: [
        { text: 'All Campaigns', value: 1 },
        { text: '24-7miamilocksmith.com', value: 2 },
        { text: 'jacksonvilleapplianceexperts.com', value: 3 },
        { text: 'samedayapplianceservice.net', value: 4 }
      ],
      filterDate: 3,
      filterDates: [
        { text: 'Today', value: 1 },
        { text: 'Yesterday', value: 2 },
        { text: 'Last 7 Days', value: 3 },
        { text: 'Last 7 Days + Today', value: 4 },
        { text: 'Last 14 Days', value: 5 },
        { text: 'Last 30 Days', value: 6 },
        { text: 'Last 60 Days', value: 7 },
        { text: 'Last 90 Days', value: 8 },
        { text: 'This Month', value: 9 },
        { text: 'Last Month', value: 10 },
        { text: 'Last Year', value: 11 },
        { text: 'This Year', value: 12 },
        { text: 'All Time', value: 13 }
      ],
      dataCollection: null,
      chartOptions
    }
  },
  created () {
    this.fillStatsData()
  },
  mounted () {
    this.$nextTick(() => {
      document.getElementById('line-chart').style.height = '250px'
    })
  },
  methods: {
    fillStatsData () {
      this.dataCollection = {
        labels: ['', 'Sunday (10-11)', 'Monday (10-12)', 'Tuesday (10-13)', 'Wednesday (10-14)', 'Thursday (10-15)', 'Friday (10-16)', 'Saturday (10-17)', ''],
        datasets: [
          {
            label: '24-7miamilocksmith.com',
            borderColor: 'green',
            backgroundColor: 'transparent',
            pointBackgroundColor: 'green',
            pointRadius: 4,
            lineTension: 0,
            data: [null, 0, 0, 0, 0, 0, 0, 0, null]
          },
          {
            label: 'jacksonvilleapplianceexperts.com',
            borderColor: 'red',
            backgroundColor: 'transparent',
            pointBackgroundColor: 'red',
            pointRadius: 4,
            lineTension: 0,
            data: [null, 1, 4, 2, 6, 5, 4, 2, null]
          },
          {
            label: 'samedayapplianceservice.net',
            borderColor: '#ff9900',
            backgroundColor: 'transparent',
            pointBackgroundColor: '#ff9900',
            pointRadius: 4,
            lineTension: 0,
            data: [null, 0, 1, 0, 0, 2, 0, 0, null]
          }
        ]
      }
    }
  }
}
</script>
<style lang="scss" scoped>
@import "@/assets/scss/variable.scss";
.stats-graph {
  background: $statsGraphBgColor;
}
::v-deep .v-label {
  font-size: $FS12 !important;
}
</style>
