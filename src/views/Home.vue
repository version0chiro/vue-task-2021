<template>
    <div v-show="showAddTask">
        <AddTask @add-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
</template>

<script>
import Tasks from "../components/Tasks.vue"
import AddTask from "../components/AddTask.vue"
export default {
    name: 'Home',
    components: {
        Tasks, AddTask
    }, props: {
        showAddTask: Boolean
    }, data() {
        return {
            tasks: [],
        }

    }, methods: {
        async deleteTask(id) {
            if (confirm('Are you sure?')) {
                const response = await fetch(`/api/tasks/${id}`, {
                    method: 'DELETE'
                })
                if (response.ok) {
                    this.tasks = this.tasks.filter(task => task.id !== id)
                } else {

                    alert('Something went wrong')
                }
            }

        }
        , async toggleReminder(id) {

            const taskToUpdate = this.tasks.find(task => task.id === id)
            const response = await fetch(`/api/tasks/${id}`, {
                method: 'PATCH',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    reminder: !taskToUpdate.reminder
                })
            })
            if (response.ok) {
                taskToUpdate.reminder = !taskToUpdate.reminder
            } else {
                alert('Something went wrong')
            }


        }, async addTask(task) {
            // console.log(task);
            const res = await fetch('api/tasks/', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(task)

            })

            const data = await res.json();
            this.tasks = [...this.tasks, data]
        }, async fetchTasks() {
            const res = await fetch('api/tasks')

            const data = await res.json()

            return data;
        }, async fetchTask(id) {
            const res = await fetch(`api/tasks/${id}`)

            const data = await res.json()

            return data;
        }
    }
    , async created() {
        this.tasks = await this.fetchTasks()
    }
}



</script>

<style>
</style>