<template>
    <div>
        <trading-vue :data="dc" :toolbar="true" ref="tradingVue"></trading-vue>
    </div>
</template>

<script>
    import TradingVue from 'trading-vue-js';
    import {DataCube} from "trading-vue-js";
    import data from "./quotes";

    export default {
        name: 'MemoryLeak',
        components: {
            TradingVue
        },
        mounted() {
            let index = 0;
            let that = this;
            const interval = setInterval(function () {
                if (index === data.quotes.length-1) {
                    clearInterval(interval)
                }
                that.updateChart(data.quotes.slice(0, index))
                index++
            }, 10)
        },
        methods: {
            updateChart(newData) {
                if (this.$refs.tradingVue && this.dc.data.chart.data.length) {
                    // 1 case - without memory leak
                    // this.$refs.tradingVue.goto(this.dc.data.chart.data[this.dc.data.chart.data.length - 1][0])

                    // 2 case - with memory leak
                    this.$refs.tradingVue.resetChart()
                }
                this.dc.merge('chart.data', newData)
            }
        },
        data() {
            return {
                dc: new DataCube({
                    chart: {
                        data: [],
                        indexBased: true,
                        tf: "5m",
                    },
                })
            }
        }
    }
</script>
