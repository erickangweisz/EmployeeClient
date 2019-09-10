<template>
  <v-app>
    
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Employee</span>
        <span class="font-weight-light">|VUETIFY<span style="color: #1697F6">&</span>AXIOS
        </span>
      </v-toolbar-title>
    </v-app-bar>

    <v-content>
      <router-view/>
    </v-content>

  </v-app>
</template>

<script>
import Home from './components/Home'

export default {
  name: 'App',
  components: {
    Home
  },
  data: () => ({
    //
  })
}
</script>
