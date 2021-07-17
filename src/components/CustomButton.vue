<template>
    <button v-on:click="addTask()" v-bind:style="{background: color}">{{ text }}</button>
</template>

<script>

export default {
    name: 'CustomButton',
    props: {
        text: String,
        color: String
    },
    methods: {
        addTask() {
            console.log("Add Task Clicked");
        }
    }
}
</script>

<style scoped>
    button {
        background: #000;
        color: #fff;
        padding: 10px 20px;
        border-radius: 5px;
        border: none;
    }
    button:hover {
        cursor: pointer;
    }
</style>