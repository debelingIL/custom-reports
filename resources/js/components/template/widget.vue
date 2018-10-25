<template>
    <div class="col-sm-12">
        <div class="card widget">
            <div v-if="widgetData.context" class="row">
                <div class="card-body">
                    <h1 class="card-title">{{widgetData.title}}</h1>
                    <table class="table" v-if="widgetData.textOptions">
                        <tbody>
                            <tr v-for="(option, key) in widgetData.textOptions" :key="key">
                                <td>{{option.title}}</td>
                                <td>{{option.text}}</td>
                            </tr>
                        </tbody>
                    </table>
                    <div v-if="widgetData.title" class="btn btn-primary" @click="emitDetails">Customize</div>
                </div>
            </div>
            <div v-else class="row">
                <div class="col-sm-7">
                    <div class="card-body">
                        <h4 class="card-title">{{widgetData.title}}</h4>
                        <table class="table" v-if="widgetData.textOptions">
                            <tbody>
                                <tr v-for="(option, key) in widgetData.textOptions" :key="key">
                                    <td>{{option.title}}</td>
                                    <td>{{option.text}}</td>
                                </tr>
                            </tbody>
                        </table>
                        <div v-if="widgetData.title" class="btn btn-primary" @click="emitDetails">Customize</div>
                    </div>
                </div>
                <div class="col-sm-5">
                    <g-chart v-if="widgetData.chart" :type="widgetData.chart.type" :data="widgetData.chart.data" :options="widgetData.chart.options" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { GChart } from 'vue-google-charts';

    export default {
        components: {
            GChart
        },
        props: {
            "widget-data": Object
        },
        methods: {
            emitDetails: function () {
                this.$emit('details');
            }
        }
    }
   
</script>

<style scoped>

</style>