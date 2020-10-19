<template>
  <v-app>
    <Navbar />
    <transition>
      <router-view></router-view>
    </transition>
  </v-app>
</template>

<script>
import Navbar from './components/Navbar'

export default {
  name: 'App',

  components: {
    Navbar
  },

  data: () => ({
    //
  })
}
</script>
