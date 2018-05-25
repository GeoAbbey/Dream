<template>
<v-container grid-list-md>
  <h2 class="mb-4" style="color: #757575">Dashboard</h2>
  <v-spacer></v-spacer>
  <v-layout row wrap>
    <v-flex md12 xs12>
      <v-card class="pa-3">
        <line-chart :height="300"></line-chart>
      </v-card>
    </v-flex>
    <v-flex md6 xs12 class="my-2">
      <v-card class="pa-3">
        <doughnut-chart></doughnut-chart>
      </v-card>
    </v-flex>
    <v-flex md6 xs12 class="my-2">
      <v-card class="pa-3">
        <polar-area-chart></polar-area-chart>
      </v-card>
    </v-flex>
    <v-flex md12 xs12>
      <v-card class="pa-3">
        <bar-chart :height="150"></bar-chart>
      </v-card>
    </v-flex>
    <v-flex md6 xs12 class="my-2">
      <v-card class="pa-3">
        <radar-chart></radar-chart>
      </v-card>
    </v-flex>
    <v-flex md6 xs12 class="my-2">
      <v-card class="pa-3">
        <pie-chart></pie-chart>
      </v-card>
    </v-flex>
  </v-layout>
</v-container>
</template>

<script>
import BarChart from '~/components/charts/BarChart'
import LineChart from '~/components/charts/LineChart'
import DoughnutChart from '~/components/charts/DoughnutChart'
import RadarChart from '~/components/charts/RadarChart'
import PieChart from '~/components/charts/PieChart'
import PolarAreaChart from '~/components/charts/PolarAreaChart'

export default {
  name: 'charts',
  components: {
    BarChart,
    LineChart,
    DoughnutChart,
    RadarChart,
    PieChart,
    PolarAreaChart
  }
}
</script>