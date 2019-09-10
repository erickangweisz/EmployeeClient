<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    :items-per-page="5"
    class="elevation-1"
  ></v-data-table>
</template>

<script>
import axios from 'axios'

export default {
    name: 'employee-table',
    data () {
        return {
            employees: null,
            headers: [
                { text: 'Id', value: 'id' },
                { text: 'Firstname', value: 'firstname' },
                { text: 'Lastname', value: 'lastname' },
                { text: 'Email', value: 'email' },
                { text: 'Cellphone', value: 'cellphone' }
            ],
            desserts: this.employees
        }
    },
    mounted () {
        axios
            .get(`https://localhost:44349/api/employee`)
            .then(response => { 
                this.employees = response['data']
                console.log(this.employees)
            })
    }
}
</script>