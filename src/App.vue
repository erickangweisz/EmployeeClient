<template>
  <v-app>
    
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Employees</span>
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
export default {
  name: 'App',
  components: {
    
  },
  data: () => ({
    
  })
}
</script>
