<template>
    <div :key="task.id" v-for="task in tasksInside">
        <!-- <h3>
            {{ task.text }}
        </h3> -->
        <!-- further reading -->
        <Task @toggle-reminder = "$emit('toggle-reminder',task.id)" @delete-task1="$emit('delete-task2',task.id)" :taskHere = "task"/>
    </div>
</template>
<script>
import Task from './Task'
    export default{
        name: 'Tasks',
        props: {
            tasksInside: Array,
        },
        components: {
            Task
        },
        // emits: ['delete-task2','delete-task1']
        // further reading
        emits: ['delete-task2','delete-task1','toggle-reminder']
    }
</script>
