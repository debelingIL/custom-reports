<template>
    <div class="col-sm-12 deets">
        <div class="row" v-if="details.title">
            <h4>Widget title</h4>
            <at-ta :members="members" class="title-edit">
                <textarea class="form-control" :name="details.title" cols="10" rows="1" v-model="details.title"></textarea>
            </at-ta>
            <!-- <input type="text" id="widgetTitle" class="form-control" v-model="details.title"> -->
        </div>
        <div class="row" v-if="details.chart.type">
            <div class="col-sm-12">
                <h4>Widget chart</h4>
                <h5>Chart Type</h5>
                <label v-for="(type, key) in details.chart.typeOptions" :key="key" style="display:block">
                    <input type="radio" :value="type" v-model="details.chart.type">
                    {{type}}
                    <br>
                </label>
                
                <h5>Chart Colors</h5>
                <label v-for="(colors) in details.chart.colorOptions" :key="colors[0]" style="display:block">
                    <input type="radio" :value="colors" v-model="details.chart.options.colors">
                    <div v-for="(color) in colors" :key="color" class="color-square" :style="{background: color}">
                    </div>
                    <br>
                </label>
            </div>
        </div>
        <div class="row" v-if="details.textOptions.length">
            <div class="col-sm-12">
                <h4>Widget text</h4>
                <div class="text-option" v-for="(option, key) in details.textOptions" :key="key">
                    <label :for="option.id">{{option.title}}</label>
                    <!-- <textarea class="form-control" :name="option.id" :id="option.id" cols="5" rows="3" v-model="option.text"></textarea> -->
                    <!-- <at :members="members" v-model="option.text">
                        <div contenteditable class="editor"></div>
                    </at> -->
                    <at-ta :members="members">
                        <textarea class="form-control" :name="option.id" :id="option.id" cols="5" rows="3" v-model="option.text" @change="highlightText(option.text)"></textarea>
                    </at-ta>
                </div>
            </div> 
        </div>
    </div>
</template>

<script>
    import at from 'vue-at'
    import AtTa from 'vue-at/dist/vue-at-textarea'

    export default {
        components: {
            at,
            AtTa
        },
        props: {
            details: Object
        },
        data: function () {
            return {
                selected: "",
                color: "",
                members: ["student_name", "teacher_name", "class_name"],
                currentText: ""
            }
        },
        watch: {
            currentText: function (newText) {
                newText.replace(new RegExp('/[@]\w+', 'gi'), match => {
                    return '<span class="keyWord">' + match + '</span>';
                })
            }
        },
        methods: {
            highlightText: function (newText) {
                newText.replace(new RegExp('/[@]\w+', 'gi'), match => {
                    console.log('<span class="keyWord">' + match + '</span>');
                    return '<span class="keyWord">' + match + '</span>';
                })
            }
        }
    }
</script>

<style scoped>
.deets {
    padding: 20px;
}
.row {
    margin-top: 20px;
}
.row:first-of-type {
    margin-top: 0;
}
.keyWord {
    background-color: aqua;
}
.title-edit {
    position: relative;
    width: 100%;
}
.color-square {
    height: 12px;
    width: 12px;
    display: inline-block;
}
</style>