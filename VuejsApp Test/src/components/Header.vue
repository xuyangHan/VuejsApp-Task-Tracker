<template>
    <header>
        <h2>{{ title }}</h2>
        <button type="button"
                :class="showAddTask ? 'btn btn-danger' : 'btn btn-info'"
                @click="onClick()">
            {{ showAddTask ? 'Close' : 'Add Task' }}
        </button>
    </header>
</template>

<script>
    export default {
        name: 'Header',
        props: {
            title: String,
            showAddTask: Boolean,
        },
        methods: {
            onClick() {
                this.$emit('toggle-add-task')
            },
        }
    }
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }

    h2 {
        color: #426696;
        font-weight: 600;
        font-size: 3rem;
        opacity: 0.8;
    }
</style>