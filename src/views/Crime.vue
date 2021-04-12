<template>
    <div>
        <h1>Crime</h1>

        <div v-if="pleaseWait" class="text-warning">
            <h3>Please wait...</h3>
        </div>

        <table class="table table-striped table-bordered">
            <thead>
                <tr>
                    <th>geography</th>
                    <th>year</th>
                    <th>violations</th>
                    <th>incidents</th>
                    <th>rates</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="incident in incidents" :key="incident.year">
                    <td>{{incident.geography}}</td>
                    <td>{{incident.year}}</td>
                    <td>{{incident.violations}}</td>
                    <td>{{incident.incidents}}</td>
                    <td>{{incident.rates}}</td>
                </tr>
            </tbody>
        </table>

    </div>
</template>

<style scoped>
    .table { 
        padding: 20px; width: 80%; margin: auto; 
    }
</style>

<script>

import axios from 'axios'

export default {
    name: 'Crime',
    data () {
        return {
            incidents: [],
            errors: [],
            pleaseWait: false
        }
    },
    created () {
        this.getData()
    },
    methods: {
        getUrl() {
            return 'https://data.novascotia.ca/resource/daey-6b54.json'
        },
        getData () {
            axios.get(this.getUrl())
            .then(response => {
                this.incidents = response.data
            })
            .catch(e => {
                this.errors.push(e)
            })
       }
    }
}
</script>