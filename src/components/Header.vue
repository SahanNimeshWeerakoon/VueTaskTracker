<template>
    <header>
        <h1>{{ title }}</h1>
        <CustomButton @toggle-add-task="$emit('toggle-add-task')" text="Add Task" color="green" />
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
        }
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