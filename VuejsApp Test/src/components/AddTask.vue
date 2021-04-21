<template>
    <form @submit="onSubmit" class="add-form">
        <div class="form-group">
            <label>Task</label>
            <input class="form-control" type="text" v-model="text" name="text" placeholder="Add Task" />
        </div>
        <div class="form-group">
            <label>Day & Time</label>
            <input class="form-control"
                   type="text"
                   v-model="day"
                   name="day"
                   placeholder="Add Day & Time" />
        </div>
        <div class="form-check">
            <input class="form-control-check form-check-input" type="checkbox" v-model="reminder" name="reminder" />
            <label class="form-check-label">Set Reminder</label>            
        </div>

        <input type="submit" value="Save Task" class="btn btn-dark" />
    </form>
</template>

<script lang="ts">
    export default {
        name: 'AddTask',
        data() {
            return {
                text: '',
                day: '',
                reminder: false,
            }
        },
        methods: {
            onSubmit(e) {
                e.preventDefault()
                if (!this.text) {
                    alert('Please add a task')
                    return
                }
                const newTask = {
                    // id: Math.floor(Math.random() * 100000),
                    text: this.text,
                    day: this.day,
                    reminder: this.reminder,
                }
                this.$emit('add-task', newTask)
                this.text = ''
                this.day = ''
                this.reminder = false
            },
        },
    }
    
</script>

<style scoped>
    .add-form {
        margin-bottom: 40px;
    }

    .form-group label {
        display: block;
        color: #426696;
        font-weight: 600;
        opacity: 0.8;
    }

    .form-check-label {
        display: block;
        color: #426696;
        font-weight: 600;
        opacity: 0.8;
    }
</style>