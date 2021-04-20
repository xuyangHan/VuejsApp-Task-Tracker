<template>
    <header>
        <h2>{{ title }}</h2>
        <button
                type="button" 
                class="btn btn-info" 
                @click="onClick()"
                >Add Task</button>
    </header>
</template>

<script>

    export default {
        name: 'Header',
        props: {
            title: String,
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
</style>