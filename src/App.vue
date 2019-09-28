<template>
  <v-app color="#fafafa">
      <Navbar/>
    <v-content class=" mb-4">
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>
import Navbar from '@/components/Navbar.vue'

export default {
  name: 'App',
  components: { Navbar, },
  data: () => ({
    //
  }),
};
</script>

<style scoped>

</style>