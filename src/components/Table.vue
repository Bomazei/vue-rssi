<template>
    <div class="wrapper">
        <table class="table">
            <thead>
            <tr>
                <th>ФИО</th>
                <th>МАС</th>
                <th>Телефон</th>
            </tr>
            </thead>
        <tbody>
            <tr v-for="(user,index) in users" @click="inspect(user.signals, index)" :key="index">
                <td>{{user.first_name + ' ' + user.last_name}}</td>
                <td>{{user.mac}}</td>
                <td>{{user.phone}}</td>
            </tr>
        </tbody>
        </table>
        <UserChart :user = inspected :userId = userId></UserChart>
        
        
    </div>
</template>

<script>
import Chart from 'chart.js';
import UserChart from './UserChart'
export default {
    components: {
        UserChart
    },
    data() {
        return {
            users: [],
            userId: '',
            inspected: []
        }
    },
    beforeMount(){
        fetch('https://cors-anywhere.herokuapp.com/' + 'https://rssi.wmrk.tk/')
            .then(response => response.json())
            .then(json => this.users = json)
        
    },
    methods: {
        inspect: function (user, userId) { 
            this.inspected = user
            this.userId = userId
        }
    }
}
</script>

<style>

</style>