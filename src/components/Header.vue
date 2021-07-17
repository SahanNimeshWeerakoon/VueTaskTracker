<template>
    <header>
        <h1>{{ title }}</h1>
        <CustomButton @btn-click="$emit('toggle-add-task')" :text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : 'green'" />
    </header>
</template>

<script>
import CustomButton from './CustomButton'

export default {
    name: 'Header',
    props: {
        title: {
            type: String,
            default: 'Hello World'
        },
        showAddTask: Boolean
    },
    components: {
        CustomButton
    },
    emits: ['toggle-add-task']
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