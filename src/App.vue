<template>
  <v-app>
    <Navbar />
    <v-main class="ma-6">
      <StatsGraph />
      <CallHistory />
    </v-main>
  </v-app>
</template>

<script>
import Navbar from './components/Navbar'
import StatsGraph from './components/StatsGraph'
import CallHistory from './components/CallHistory'

export default {
  name: 'App',

  components: {
    Navbar,
    StatsGraph,
    CallHistory
  },

  data: () => ({
    //
  })
}
</script>
