<template>
    <header>
        <h1>{{ title }}</h1>
        <Button
            @btn-click="$emit('toggle-add-task')"
            :text="showAddTask ? 'Close' : 'Add Task'"
            :color="showAddTask ? 'red' : 'green'"
        />       
        <Button
            @btn-click="$emit('toggle-update-task')"
            :text="showUpdateTask ? 'Close' : 'Update Task'"
            :color="showUpdateTask ? 'red' : 'green'"
        />  
        
        <!-- <Button text="Update Task" color="blue"/>
        <Button text="Delete Task" color="red" /> -->
    </header>
</template>

<script>
import Button from './Button'

    export default {
        name: 'Header',
        props : {
            title: String,
            showAddTask: Boolean,
            showUpdateTask: Boolean
    },
        components: {
            Button
        }
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