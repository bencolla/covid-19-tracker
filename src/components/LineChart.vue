<script>
    //Importing Line class from the vue-chartjs wrapper
    import { Line } from 'vue-chartjs'

    //Exporting this so it can be used in other components
    export default {
        extends: Line,
        props: ['infected', 'dates'],
        data () {
            return {
                datacollection: {
                    //Data to be represented on x-axis
                    labels: this.dates,
                    datasets: [
                        {
                            label: 'Infected',
                            backgroundColor: '#f87979',
                            pointBackgroundColor: 'white',
                            borderWidth: 1,
                            pointBorderColor: '#249EBF',
                            //Data to be represented on y-axis
                            data: this.infected
                        }
                    ]
                },
                //Chart.js options that controls the appearance of the chart
                options: {
                    scales: {
                        yAxes: [{
                            ticks: {
                                beginAtZero: true
                            },
                            gridLines: {
                                display: true
                            }
                        }],
                        xAxes: [ {
                            gridLines: {
                                display: false
                            }
                        }]
                    },
                    legend: {
                        display: true
                    },
                    responsive: true,
                    maintainAspectRatio: true
                }
            }
        },
        mounted () {
            //renderChart function renders the chart with the datacollection and options object.
            setTimeout(() => {this.renderChart(this.datacollection, this.options)}, 250);
        }
    }
</script>