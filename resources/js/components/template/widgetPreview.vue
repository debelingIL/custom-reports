<template>
    <div class="col-sm-12">
        <div class="card widget">
            <div class="row">
                <div class="col-sm-7">
                    <div class="card-body">
                        <h5 class="card-title">{{widgetData.preview.title}}</h5>
                        <div class="card-text">{{widgetData.preview.description}}</div>
                    </div>
                </div>
                <div class="col-sm-5">
                    <img :src="widgetData.preview.image" class="img-fluid" alt="">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            "widget-data": Object
        }
    }
</script>

<style scoped>

</style>