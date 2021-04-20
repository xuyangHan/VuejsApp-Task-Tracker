<template>
    <div class="home">
        <div class="container">
            <Header
                    @toggle-add-task="toggleAddTask" 
                    title="Task Tracker"
                    :showAddTask="showAddTask"
                    />
            <div v-show="showAddTask">
                <AddTask @add-task="addTask" />
            </div>
            
            <Tasks @toggle-reminder="toggleReminder"
                   @delete-task="deleteTask"
                   :tasks="tasks">
            </Tasks>
        </div>
    </div>
</template>

<script>
    import Header from './Header'
    import Tasks from './Tasks'
    import AddTask from './AddTask'

    export default {
        name: 'Home',
        components: {
            Header,
            Tasks,
            AddTask,
        },
        data() {
            return {
                tasks: [],
                showAddTask: false
            }
        },
        methods: {
            toggleAddTask() {
                this.showAddTask = !this.showAddTask;
    
            },
            addTask(task) {
                this.tasks = [...this.tasks, task]
            },
            deleteTask(id) {
                if (confirm('Are you sure to delete the task?')) {
                    this.tasks = this.tasks.filter((task) => task.id !== id)

                }
            },
            toggleReminder(id) {
                this.tasks = this.tasks.map((task) =>
                    task.id === id ? { ...task, reminder: !task.reminder } : task
                )
            }
        },
        created() {
            this.tasks = [
                {
                    id: 1,
                    text: 'vue.js tutorial',
                    day: '2021/4/20',
                    reminder: true,
                },
                {
                    id: 2,
                    text: 'GIS Preparation',
                    day: '2021/4/25',
                    reminder: true,
                },
                {
                    id: 3,
                    text: 'Angular + .NET Core + GIS JS API',
                    day: '2021/4/30',
                    reminder: false,
                },
            ]
        }
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

