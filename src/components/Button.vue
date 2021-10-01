<template>
    <button @click="$emit('toggle-add-task')" :style="{ background: color }" class="btn">{{ text }}</button>
</template>

<script>

export default {
    name: 'Button',
    props: {
        text: {
            type: String,
            default: 'Add Task',

        }, color: {
            type: String,
            default: 'green'
        }, emits: [
            'toggle-add-task'
        ]
    }
}
</script>