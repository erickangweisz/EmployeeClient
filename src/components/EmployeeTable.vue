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
            url: 'https://localhost:44349/api/employee',
            headers: [
                { text: 'Id', value: 'id' },
                { text: 'Firstname', value: 'firstname' },
                { text: 'Lastname', value: 'lastname' },
                { text: 'Email', value: 'email' },
                { text: 'Cellphone', value: 'cellphone' }
            ],
            desserts: []
        }
    },
    methods: {
        getEmployees() {
            axios
                .get(this.url)
                .then(response => this.desserts = response.data)
                .catch(console.error = (message) => { // eslint-disable-line no-console
                    throw new Error(message)
                })
        }
    },
    mounted () {
        this.getEmployees()
    }
}
</script>