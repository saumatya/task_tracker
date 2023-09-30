<template>
    <!-- further reading -->
    <div @dblclick="$emit('toggle-reminder', taskHere.id)" :class="[taskHere.reminder ? 'reminder' : '', 'task']">
    <!-- <div class="task"> -->
        <h3>
            {{ taskHere.text }} 
            <i @click="onDelete(taskHere.id)" class="fas fa-times"></i>
        </h3>
        <p>{{ taskHere.day }}</p>
    </div>
    
</template>
<script>
export default {
    name: 'Task',
    props: {
        taskHere : Object
    }, 
    methods: {
        onDelete(id)
        {
            console.log('inside task',id)
            this.$emit('delete-task1',id)
        },
    }
}

</script>
<style scope>
.fas {
    color: red;
}
.task{
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}
.task.reminder {
    border-left: 5px solid green;
}
.task h3{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>