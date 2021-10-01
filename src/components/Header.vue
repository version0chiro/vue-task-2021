<template>
    <header>
        <h1>{{ title }}</h1>
        <Button @click="onClick()" text="Add Task" color="green" />
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
        }
    }, components: {
        Button
    }, methods: {
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