<template>
    <div class="container-fluid">
        <div class="row">
            <nav class="nav template-nav justify-content-end">
                <a class="nav-link active align-middle" href="#">Share template</a>
                <a href="/report" class="nav-link">Create report</a>
            </nav>
        </div>
        <div class="row">
            <div class="col-sm-3">
                <div class="template-col">
                    <draggable v-model="previewArray" :options="{group:'widgets'}">
                        <transition-group>
                            <widget-preview v-for="(item, key) in previewArray" :key="key" :widget-data="item"> </widget-preview>
                        </transition-group>
                    </draggable>
                </div>
            </div>
            <div class="col-sm-6">
                <div class="template-col">
                    <draggable v-model="templateArray" :options="{group:'widgets'}">
                        <transition-group>
                            <widget v-for="(item, key) in templateArray" 
                            :key="key" 
                            :widget-data="item" 
                            @details="displayWidgetDetails(item)"> 
                            </widget>
                        </transition-group>
                    </draggable>
                    <div class="card">
                        <div class="card-body">
                            Drag report widgets here!
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-sm-3">
                <div class="template-col">
                    <widget-details :details="selectedWidget"> </widget-details>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import draggable from 'vuedraggable';
    import widget from './widget';
    import widgetPreview from './widgetPreview';
    import widgetDetails from './widgetDetails';
    

    export default {
        components: {
            draggable,
            widget,
            widgetPreview,
            widgetDetails,
        },
        mounted() {
            console.log('Component mounted.')
        },
        data: function () {
            return {
                previewArray: [
                    {
                        preview: {
                            title: "Student by class",
                            description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. ",
                            image: "https://via.placeholder.com/300"
                        },
                        title: "Student by class",
                        chart: {
                            type: "BarChart",
                            typeOptions: [
                                "ColumnChart",
                                "BarChart",
                                "BubbleChart"
                            ],
                            data: [
                                ['Year', 'Sales', 'Expenses', 'Profit', 'Something'],
                                ['2014', 1000, 400, 200, 220],
                                ['2015', 1170, 460, 250, 220],
                                ['2016', 660, 1120, 300, 220],
                                ['2017', 1030, 540, 350, 220]
                            ],
                            colorOptions: [
                                ["#ffeaa7", "#81ecec", "#74b9ff"],
                                ["#55efc4", "#ff7675", "#e84393"]
                            ],
                            options: {
                                colors: ["#55efc4", "#81ecec", "#74b9ff"],
                                chart: {
                                    title: "Test Chart",
                                    subtitle: "Subtitle"
                                }
                            }
                        },
                        textOptions: [
                            {
                                title: "Above level",
                                id: "aboveLevel",
                                text: "This is the above level text"
                            },
                            {
                                title: "At level",
                                id: "atLevel",
                                text: "This is the at level text"
                            },
                            {
                                title: "Below level",
                                id: "belowLevel",
                                text: "This is the below level text"
                            },
                            {
                                title: "Well below level",
                                id: "wellBelowLevel",
                                text: "This is the well below level text"
                            },
                            
                        ]
                    },
                    {
                        preview: {
                            title: "Student by assessment",
                            description: "Consectetur adipiscing elit. Nisi viverra semper.",
                            image: "https://via.placeholder.com/300"
                        },
                        title: "Studeny by assessment",
                        description: "Something else",
                        chart: {
                            type: "LineChart",
                            typeOptions: [
                                "ColumnChart",
                                "BarChart",
                                "LineChart"
                            ],
                            data: [
                                ['Year', 'Sales', 'Expenses', 'Profit'],
                                ['2014', 1000, 400, 200],
                                ['2015', 1170, 460, 250],
                                ['2016', 660, 1120, 300],
                                ['2017', 1030, 540, 350]
                            ],
                            colorOptions: [
                                ["#ffeaa7", "#81ecec", "#74b9ff"],
                                ["#55efc4", "#ff7675", "#e84393"]
                            ],
                            options: {
                                colors: ["#55efc4", "#81ecec", "#74b9ff"],
                                chart: {
                                    title: "Test Chart",
                                    subtitle: "Subtitle"
                                }
                            }
                        },
                        textOptions: [
                            {
                                title: "Only one text option",
                                id: "desction",
                                text: "This is a widget with only one description."
                            },
                            
                        ]
                    },
                    {
                        preview: {
                            title: "Student by standard",
                            description: "Nunc congue felis et nisi viverra semper.",
                            image: "https://via.placeholder.com/300"
                        },
                        title: "Student by standard",
                        description: "Something else",
                        chart: {
                            type: "LineChart",
                            typeOptions: [
                                "ColumnChart",
                                "BarChart",
                                "AreaChart"
                            ],
                            colorOptions: [
                                ["#ffeaa7", "#81ecec", "#74b9ff"],
                                ["#55efc4", "#ff7675", "#e84393"]
                            ],
                            data: [
                                ['Year', 'Sales', 'Expenses', 'Profit'],
                                ['2014', 1000, 400, 200],
                                ['2015', 1170, 460, 250],
                                ['2016', 660, 1120, 300],
                                ['2017', 1030, 540, 350]
                            ],
                            options: {
                                colors: ["#55efc4", "#81ecec", "#74b9ff"],
                                chart: {
                                    title: "Test Chart",
                                    subtitle: "Subtitle"
                                }
                            }
                        },
                        textOptions: [
                            {
                                title: "At level",
                                id: "atLevel",
                                text: "This is the at level text"
                            },
                            {
                                title: "Below level",
                                id: "belowLevel",
                                text: "This is the below level text"
                            }
                            
                        ]
                    }
                ],
                templateArray: [
                    {
                        preview: {
                            title: "",
                            description: "",
                            image: ""
                        },
                        title: "SEP Report",
                        context: true,
                        chart: {},
                        textOptions: [
                            {
                                title: "Report description",
                                id: "description",
                                text: "This is a parent-teacher report which will help your student do good better. We hope you enjoy this beautiful report builder."
                            },
                            {
                                title: "Name of teacher filling the report",
                                id: "teacher",
                                text: "@teacher_name"
                            },
                            {
                                title: "Name of class for the desired student",
                                id: "class",
                                text: "@class_name"
                            },
                            {
                                title: "Name of student on the report",
                                id: "student",
                                text: "@student_name"
                            }
                        ]
                    },
                ],
                selectedWidget: {
                    preview: {
                        title: "",
                        description: "",
                        image: ""
                    },
                    title: "",
                    chart: {
                        type: "",
                        typeOptions: [],
                        data: [],
                        options: {
                            chart: {
                                title: "",
                                subtitle: ""
                            }
                        }
                    },
                    textOptions: []
                }
            }
        },
        methods: {
            displayWidgetDetails: function (item) {
                this.selectedWidget = item;
            }
        }
    }
</script>

<style scoped>
.template-nav {
    margin-left: 20px;
    margin-right: 20px;
    height: 60px;
    width: 100%;
    background-color: white;
    border-radius: 10px;
}
.nav-link {
    position: relative;
    top: 10px;
}
.template-col {
    margin-top: 20px;
    background-color: white;
    border-radius: 10px;
    min-height: 80vh;
}

.template-col:first-child {
    margin-left: 20px;
    margin-right: 0;
}

</style>

