<template>
    <div class="container-fluid">
        <div class="row col-sm-9">
            <nav class="nav template-nav justify-content-end">
                <a href="#" class="nav-link">Export report</a>
                <a href="#" class="nav-link">Share report</a>
                <a href="#" class="nav-link align-middle">Print</a>
            </nav>
        </div>
        <div class="row">
            <div class="col-sm-3">
                <div class="template-col">
                    <h4>Export Options</h4>
                    <div class="row">
                        <div class="col-sm-12">
                            <multiselect
                                :options="options"
                                :multiple="true"
                                label="name"
                                group-label="class"
                                group-values="students"
                                :group-select="true"
                                track-by="name"
                                placeholder="Select student"
                                v-model="selected"> 
                                <template 
                                    slot="selection" 
                                    slot-scope="{ values, search, isOpen }">
                                    <span class="multiselect__single" v-if="values.length &amp;&amp; !isOpen">
                                        {{ values.length }} students selected
                                    </span>
                                </template>
                            </multiselect>
                            <div class="selected" v-if="selected">
                                <student v-for="(student, key) in selected" :key="key" :student="student" @removeStudent="removeStudent"></student>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-sm-6">
                <div class="template-col report-preview">
                    <h4>Report preview</h4>
                    <p>Select students to see a preview of the report</p>
                    <report v-for="(student, key) in selected" :key="key" :student="student" :report="report" class="report-widget"></report>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import draggable from 'vuedraggable';
    import multiselect from 'vue-multiselect';
    import report from './report';
    import student from './student';
    import { SweetModal, SweetModalTab } from 'sweet-modal-vue'

    export default {
        components: {
            draggable,
            multiselect,
            report,
            student,
            SweetModal,
		    SweetModalTab
        },
        mounted() {
            // this.$refs.modal.open()
        },
        data: function () {
            return {
                selected: null,
                options: [
                    {
                        class: 'VHS 1',
                        students: [
                            { name: "Ben Orthy", image: "https://via.placeholder.com/100", class: "VHS 1", languageOptions: ['English', 'Spanish'], language: "English", level: "atLevel"},
                            { name: "Gabriel Jesus", image: "https://via.placeholder.com/100", class: "VHS 1", languageOptions: ['English', 'Spanish'], language: "Spanish", level: "aboveLevel"},
                            { name: "Lionel Maradona", image: "https://via.placeholder.com/100", class: "VHS 1", languageOptions: ['English', 'Spanish'], language: "Spanish", level: "belowLevel"},
                        ]
                    },
                    {
                        class: "VHS 2",
                        students: [
                            { name: "Jen Orthy", image: "https://via.placeholder.com/100", class: "VHS 2", languageOptions: ['English', 'Spanish'], language: "English", level: "atLevel"},
                            { name: "Gabriela Jesus", image: "https://via.placeholder.com/100", class: "VHS 2", languageOptions: ['English', 'Spanish'], language: "Spanish", level: "belowLevel"},
                            { name: "Lionela Maradona", image: "https://via.placeholder.com/100", class: "VHS 2", languageOptions: ['English', 'Spanish'], language: "Spanish", level: "wellBelowLevel"},
                        ]
                    }
                ],
                report: [
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
                                text: {
                                    English: "This is the above level text",
                                    Spanish: "Sobre la tela de una araña."
                                } 
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
                                text: {
                                    English: "Something really nice about your student's data",
                                    Spanish: "Dos elefantes se balanceaban, Sobre la tela de una araña."
                                } 
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
                            type: "AreaChart",
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
                                text: {
                                    English: "Something really nice about your student's data",
                                    Spanish: "Dos elefantes se balanceaban, Sobre la tela de una araña."
                                }
                            },
                            {
                                title: "Below level",
                                id: "belowLevel",
                                text: "This is the below level text"
                            }
                            
                        ]
                    }
                ],
            }
        },
        methods: {
            removeStudent: function (student) {
                this.selected = this.selected.filter( (item) => {
                    return item.name != student.name;
                });
            }
        }
    }
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
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
    padding: 20px;
    background-color: white;
    border-radius: 10px;
    min-height: 80vh;
}

.report-preview {
    max-height: 80vh;
    overflow: scroll;
}

.template-col:first-child {
    margin-right: 20px;
    margin-left: 0;
}

.template-col:last-child {
    margin-left: 20px;
    margin-right: 0;
}

.report-widget {
    margin-bottom: 20px;
}
</style>

