<template>
    <div  class="about">
        <h2 class="text-center">{{today.Country}}</h2>
        <h3>Confirmed: <b>{{today.Confirmed}}</b></h3>
        <h3>Recovered:  <b>{{today.Recovered}}</b></h3>
        <h3>Deaths:  <b>{{today.Deaths}}</b></h3>
        <h3>Active:  <b>{{today.Active}}</b></h3>

        <line-chart  :height="250" :infected="infected" :dates="dates"></line-chart>
    </div>
</template>


<script>
    import LineChart from '@/components/LineChart'
    export default {
        components: {
            LineChart,
        },
        data() {
            return {
                infected : [],
                dates : [],
                today: ''
            }
        },
        created() {
            this.request();
        },
        mounted () {
        },
        computed: {

        },
        methods: {

            request(){
                this.$http.get('https://api.covid19api.com/country/'+localStorage.getItem('code'))
                    .then((response) => {

                        let data = []

                        response.data.forEach((line) => {
                            if(line.Province == ""){
                                data.push(line);
                            }
                        });

                        this.today = data.slice(-1).pop();
                        let options = { weekday: 'narrow', year: '2-digit', month: '2-digit', day: '2-digit' };
                        data.slice(Math.max(data.length - 9, 1)).forEach((single) =>{
                            this.infected.push(single.Active)
                            let date = new Date(single.Date).toLocaleDateString("en-US", options);
                            this.dates.push(date)
                        })
                    })
            }

        }
    }
</script>
<style>
    .text-center{
        text-align: center;
    }
</style>
