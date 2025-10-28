<script>
export default { 
    props: {
        task: {
            type: Object,
            required: true
        },
        idx: {
            type: Number,
            required: true
        }
    },
    methods: {
        markAsDone() {
            this.$emit('task-done', this.idx)
        }
    }
}
</script>

<template>
    <div class="card mb-3">
        <div class="card-body">
            <h5 class="card-title">Deadline: {{ task.deadline }}</h5>
            <hr>
            <p class="card-text">
                {{ task.desc }}
            </p>
            <button @click="markAsDone" class="btn btn-primary">Done</button>
        </div>
    </div>
</template>

<style scoped>
.card {
    max-width: 400px;
}
</style>