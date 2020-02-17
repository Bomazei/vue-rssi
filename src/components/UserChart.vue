<template>
  <div class="chart">
       <GChart v-if="user != 0"
            type="ColumnChart"
            :data="chartData"
            :options="chartOptions"
        />
        
        
  </div>
</template>

<script>
import { GChart } from 'vue-google-charts'
 

export default {
    props: ['user', 'userId'],
    components: {
        GChart
    },
    data () {
        return {
            
            id: '',
            chartOptions: {
                
                legend: { position: "none" },
                chart: {
                    title: 'Company Performance',
                    subtitle: 'Sales, Expenses, and Profit: 2014-2017',
                },
                vAxis: {
                    direction: -1
                },
                
            }
        }
    },
    updated() {
        this.id = this.userId
    },
    computed: {
        chartData: function() {
            let values = []
            function timeConverter(UNIX_timestamp){
                var a = new Date(UNIX_timestamp * 1000);
                var months = ['Янв','Фев','Мар','Апр','Май','Июн','Июл','Авг','Сен','Окт','Ноя','Дек'];
                var year = a.getFullYear();
                var month = months[a.getMonth()];
                var date = a.getDate();
                var hour = a.getHours();
                var min = "0" + a.getMinutes();
                var sec = "0" + a.getSeconds();
                var time = date + ' ' + month + ' ' + year + ' ' + hour + ':' + min.substr(-2) + ':' + sec.substr(-2) ;
                return time;
            }
            this.user.forEach((item, i) => {      
                values.push([timeConverter(item.ts), item.rssi])
            })
            values.unshift(['ms', 'rssi'])
            console.log(values)
            return values
        }
    }

}
</script>

<style>

</style>