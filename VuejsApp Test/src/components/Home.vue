<template>
    <div class="home">
        <div class="container">
            <Header title="Task Tracker"></Header>
            <Tasks :tasks="tasks"></Tasks>
        </div>
    </div>
</template>

<script>
    import Header from './Header'
    import Tasks from './Tasks'

    export default {
        name: 'Home',
        components: {
            Header,
            Tasks
        },
        data() {
            return {
                tasks: []
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

