<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex xs12>
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="150"
        ></v-img>
      </v-flex>

      <v-flex mb-4>
        <h1 class="display-2 font-weight-bold mb-3">
          CRUD Employees
        </h1>
        <p class="subheading font-weight-regular">
          With <strong>Vue.js</strong>, 
          <strong>Vuetify</strong> and 
          <strong>Axios</strong>
        </p>
      </v-flex>
    </v-layout>

    <v-layout>
      <v-flex mb-12>
        <employee-table/>
      </v-flex>
    </v-layout>

  </v-container>
</template>

<script>
import EmployeeTable from './EmployeeTable'

export default {
  data: () => ({
    
  }),
  components: {
    EmployeeTable
  }
}
</script>
