<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-2">
                <div class="card card-default">
                    <div class="card-body">
                        <p class="card-text">Create new report</p>
                        <a href="/report" class="card-link">Create</a>
                    </div>
                </div>
            </div>
            <div class="col-md-2">
                <div class="card card-default">
                    <div class="card-body">
                        <p class="card-text">Create new template</p>
                        <a href="/template" class="card-link">Create</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
