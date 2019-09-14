<template>
    <v-container>
        <v-alert 
            v-model="alert"
            type="success"
            dismissible
            v-if="alert">
            {{ alert_message }}
        </v-alert>

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
                                    label="Cellphone*" 
                                    v-model="employee.cellphone" 
                                    required></v-text-field>
                            </v-col>
                        </v-row>
                    </v-container>
                    <small>*indicates required field</small>
                </v-card-text>
                <v-divider></v-divider>
                <v-card-actions text-right>
                    <v-btn 
                        depressed 
                        color="error"
                        @click="deleteEmployee()"
                        >Delete <i class="material-icons">delete</i>
                    </v-btn>
                    <div class="flex-grow-1"></div>
                    <v-btn 
                        color="blue darken-1" 
                        text 
                        @click="dialog=false"
                        >Close <i class="material-icons">clear</i>
                    </v-btn>
                    <v-btn 
                        color="blue darken-1" 
                        ext 
                        @click="updateEmployee()"
                        >Save <i class="material-icons">save</i>
                    </v-btn>
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
            employee: {},
            dialog: false,
            alert: false,
            alert_message: ''
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
                .then(response => { 
                    this.employee = response 
                    this.dialog = false
                    this.alert_message = 'The employee has been updated!'
                    this.alert = true
                })
                .catch(console.error = (message) => { // eslint-disable-line no-console
                    throw new Error(message)
                })
        },
        deleteEmployee() {
            axios
                .delete(`${this.url}/${this.employee.id}`)
                .then(response => {
                    // TODO: pending to develop row deleting reactive in table
                    this.dialog = false
                    this.alert_message = 'The employee has been deleted!'
                    this.alert = true
                })
        }
    },
    mounted () {
        this.getEmployees()
    }
}
</script>