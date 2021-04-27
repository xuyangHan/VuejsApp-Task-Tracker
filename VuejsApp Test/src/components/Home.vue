<template>
    <div class="home">
        <div class="container">
            <Header @toggle-add-task="toggleAddTask"
                    title="Task Tracker"
                    :showAddTask="showAddTask" />
            <div v-show="showAddTask">
                <AddTask @add-task="addTask" />
            </div>

            <Tasks @toggle-reminder="toggleReminder"
                   @delete-task="deleteTask"
                   :tasks="tasks">
            </Tasks>
        </div>
        <div class="circle1"></div>
        <div class="circle2"></div>
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
            async addTask(task) {
                const res = await fetch('api/tasks', {
                    method: 'POST',
                    headers: {
                        'Content-type': 'application/json',
                    },
                    body: JSON.stringify(task),
                })

                const data = await res.json()
                this.tasks = [...this.tasks, data]
            },
            async deleteTask(id) {
                if (confirm('Are you sure to delete the task?')) {
                    const res = await fetch(`api/tasks/${id}`, {
                        method: 'DELETE'
                    })
                    res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('Error deleting task.')

                }
            },
            async toggleReminder(id) {
                const taskToToggle = await this.fetchTask(id)
                const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder }

                const res = await fetch(`api/tasks/${id}`, {
                    method: 'PUT',
                    headers: {
                        'Content-type': 'application/json',
                    },
                    body: JSON.stringify(updTask),
                })

                const data = await res.json()

                this.tasks = this.tasks.map((task) =>
                    task.id === id ? { ...task, reminder: data.reminder } : task
                )
            },
            async fetchTasks() {
                const res = await fetch(`api/tasks`)
                const data = await res.json()
                return data
            },
            async fetchTask(id) {
                const res = await fetch(`api/tasks/${id}`)
                const data = await res.json()
                return data
            }
        },
        async created() {
            this.tasks = await this.fetchTasks()
        }
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .home {
        margin: 0;
        padding: 0;
        font-family: "Poppins", sans-serif;
        min-height: 100vh;
        background: linear-gradient(to right top, #65dfc9, #6cdbeb);
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .circle1,
    .circle2 {
        background: white;
        background: linear-gradient( to right bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0.3) );
        height: 20rem;
        width: 20rem;
        position: absolute;
        border-radius: 50%;
    }

    .circle1 {
        top: 5%;
        right: 15%;
    }

    .circle2 {
        bottom: 5%;
        left: 10%;
    }

    .container {
        max-width: 800px;
        overflow: auto;
        min-height: 300px;
        padding: 30px;
        margin-top: 30px auto;
        background: white;
        min-height: 80vh;
        width: 100%;
        background: linear-gradient( to right bottom, rgba(255, 255, 255, 0.7), rgba(255, 255, 255, 0.3) );
        border-radius: 2rem;
        z-index: 2;
        backdrop-filter: blur(2rem);
    }
</style>

