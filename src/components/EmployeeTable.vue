<template>
    <v-container>
        <v-data-table
            :headers="headers"
            :items="desserts"
            :items-per-page="5"
            @click:row="getEmployee($event)"
            class="elevation-1"
        ></v-data-table>

        <v-dialog
            v-model="dialog"
            width="500">
            <v-card>
                <v-card-title>Employee</v-card-title>
                <v-card-text>
                    <v-container>
                        <v-row>
                            <v-col cols="12">
                                <v-text-field 
                                    label="Firstname*" 
                                    v-model="employee.firstname" 
                                    required></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field 
                                    label="Lastname*" 
                                    v-model="employee.lastname" 
                                    required></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field 
                                    label="Email*" 
                                    v-model="employee.email" 
                                    type="email" 
                                    required></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field 
                                    label="cellphone*" 
                                    v-model="employee.cellphone" 
                                    required></v-text-field>
                            </v-col>
                        </v-row>
                    </v-container>
                    <small>*indicates required field</small>
                </v-card-text>
                <v-divider></v-divider>
                <v-card-actions text-right>
                    <div class="flex-grow-1"></div>
                    <v-btn 
                        color="blue darken-1" 
                        text 
                        @click="dialog=false"
                        >Close</v-btn>
                    <v-btn 
                        color="blue darken-1" 
                        ext 
                        @click="updateEmployee()"
                        >Save</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-container>
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
            desserts: [],
            dialog: false,
            employee: {}
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
        },
        getEmployee(event) {
            this.dialog = true
            this.employee = event
        },
        updateEmployee() {
            axios
                .put(`${this.url}/${this.employee.id}`, this.employee)
                .then(response => this.employee = res, this.dialog = false)
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