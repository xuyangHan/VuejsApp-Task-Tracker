<template>
    <div>
        <div :key="task.id" v-for="task in tasks">
            <div @toggle-reminder="$emit('toggle-reminder', task.id)"
                 @delete-task="$emit('delete-task', task.id)"
                 :task="task">
                <div @dblclick="$emit('toggle-reminder', task.id)"
                     :class="[task.reminder ? 'reminder' : '', 'task']">
                    <h5>
                        {{ task.text }}
                        &nbsp; <i @click="$emit('delete-task', task.id)" class="fas fa-minus-circle"></i>
                    </h5>
                    <p>{{ task.day }}</p>
                </div>
            </div>                       
        </div>
    </div>
</template>

<script lang="ts">
    export default {
        name: 'Tasks',
        props: {
            tasks: Array
        },
        emits: ['delete-task', 'toggle-reminder'],
    }
</script>

<style scoped>
    .fas {
        color: red;
    }

    .task {
        
        cursor: pointer;

        display: flex;
        background: linear-gradient( to left top, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0.5) );
        border-radius: 1rem;
        margin: 2rem 0rem;
        padding: 2rem;
        box-shadow: 6px 6px 20px rgba(122, 122, 122, 0.212);
        justify-content: space-between;
    }

        .task.reminder {
            border-left: 5px solid #59ccb7;
        }

        .task h5 {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
    h5, p {
        color: #426696;
        opacity: 0.8;
    }
    h5 {
        font-weight: 600;
    }
    p {
        font-weight: 500;
    }
</style>