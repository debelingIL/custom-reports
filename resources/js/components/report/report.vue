<template>
    <div class="col-sm-12">
        <div class="card widget">
            <div v-for="(widget, key) in report" :key="key" class="row">
                <div v-if="widget.context" class="context col-sm-12">
                    <h1>{{widget.title}}</h1>
                    <table class="table">
                        <tbody>
                            <tr v-for="textOption in widget.textOptions" :key="textOption.id">
                                <td>{{textOption.id}}</td>
                                
                                <td v-if="textOption.text == '@teacher_name'">Teacher Dan</td>
                                <td v-if="textOption.text == '@class_name'">{{student.class}}</td>
                                <td v-if="textOption.text == '@student_name'">{{student.name}}</td>
                                <td v-if="textOption.id == 'description'">{{textOption.text}}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <span v-else class="col-sm-12" style="width:100%">
                    <div class="col-sm-7">
                        <div class="card-body">
                            <h4 class="card-title">{{widget.title}} {{student.name}}</h4>
                            <p v-if="widget.description">{{widget.description}}</p>
                            <div v-if="widget.textOptions" class="card-text">{{widget.textOptions[0].text[student.language]}}</div>
                        </div>
                    </div>
                    <div class="col-sm-5">
                        <g-chart v-if="widget.chart" :type="widget.chart.type" :data="widget.chart.data" :options="widget.chart.options" />
                    </div>
                </span>
                
            </div>
        </div>
    </div>
</template>

<script>
    import {GChart} from 'vue-google-charts'

    export default {
        components: {
            GChart
        },
        props: {
            report: Array,
            student: Object
        }
    }
</script>

<style scoped>

</style>