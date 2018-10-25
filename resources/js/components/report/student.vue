<template>
    <div class="col-sm-12">
        <div class="card widget">
            <div class="row">
                <div class="col-sm-4">
                    <img :src="student.image" :alt="student.name">
                </div>
                <div class="col-sm-6">
                    <div class="card-body">
                        <div class="card-title">{{student.name}}</div>
                        <label v-for="(language, key) in student.languageOptions" :key="key">
                            <input type="radio" :value="language" v-model="student.language">
                            {{language}}
                            <br>
                        </label>
                    </div>
                </div>
                <div class="col-sm-2">
                    <button class="btn btn-danger" @click="removeStudent">x</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            student: Object
        },
        methods: {
            removeStudent: function () {
                this.$emit('removeStudent', this.student);
            }
        }
    }
</script>

<style scoped>

</style>