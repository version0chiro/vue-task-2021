<template>
    <header>
        <h1>{{ title }}</h1>
        <Button
            v-show="homePage"
            @btn-click="onClick()"
            :color="showAddTask ? 'red' : 'green'"
            :text="showAddTask ? 'Close' : 'Add Task'"
        />
        <!-- <Button text="Update Task" color="blue"/> -->
        <!-- <Button text="Delete Task" color="red"/> -->
    </header>
</template>

<script>
import Button from './Button.vue'
export default {
    name: 'Header',
    props: {
        title: {
            type: String,
            default: 'Welcome to Vue.js'
        },
        showAddTask: {
            type: Boolean,
            default: false
        }
    }, components: {
        Button
    }, computed: {
        homePage() {
            if (this.$route.path === '/') {
                return true;
            } else {
                return false;
            }
        }
    },
    methods: {
        onClick() {
            this.$emit('toggle-add-task')
        }
    }, emits: ["toggle-add-task"]
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