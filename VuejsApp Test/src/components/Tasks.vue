<template>
    <div>
        <div :key="task.id" v-for="task in tasks" :class="[task.reminder ? 'reminder' : '', 'task']">
            <h5>
                {{ task.text }}
                <i @click="$emit('delete-task', task.id)" class="fas fa-minus-circle"></i>
            </h5>
            <p>{{ task.day }}</p>
        </div>
    </div>
</template>

<script lang="ts">
    export default {
        name: 'Tasks',
        props: {
            tasks: Array
        }
    }
</script>

<style scoped>
    .fas {
        color: red;
    }

    .task {
        background: #f4f4f4;
        margin: 5px;
        padding: 10px 20px;
        cursor: pointer;
    }

        .task.reminder {
            border-left: 5px solid green;
        }

        .task h5 {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
</style>