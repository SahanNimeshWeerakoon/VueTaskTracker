<template>
    <button v-on:click="$emit('btn-click')" v-bind:style="{background: color}">{{ text }}</button>
</template>

<script>

export default {
    name: 'CustomButton',
    props: {
        text: String,
        color: String
    },
    methods: {
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