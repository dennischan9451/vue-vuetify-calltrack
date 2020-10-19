<template>
  <v-main class="ma-6">
    <StatsGraph />
    <CallHistory />
  </v-main>
</template>

<script>
import StatsGraph from '@/components/StatsGraph'
import CallHistory from '@/components/CallHistory'

export default {
  name: 'Home',
  components: {
    StatsGraph,
    CallHistory
  }
}
</script>
