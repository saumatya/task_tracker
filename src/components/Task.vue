<template>
    <!-- further reading -->
    <div @dblclick="$emit('toggle-reminder', taskHere.id)" 
    :class="[taskHere.reminder ? 'reminder' : '', 'task']">
    <!-- <div class="task"> -->
        <h3>
            {{ taskHere.text }} 
            <div class="buttons">
                <i @click="onUpdate(taskHere)"
                class="fa fa-pencil" 
                aria-hidden="true"></i>
                <i @click="onDelete(taskHere.id)" class="fas fa-times"></i>               
                
            </div>
            
        </h3>
        <p>{{ taskHere.day }}</p>
    </div>
    
    <div v-show="showUpdateTask" >
      <UpdateTask @update-task="updateTask"/>
    </div> 
</template>
<script>
export default {
    name: 'Task',
    props: {
        taskHere : Object
    }, 
    data() {
    return {
      showUpdateTask:false
    }
  },
    methods: {
        onDelete(id)
        {
            console.log('inside delete task',id)
            this.$emit('delete-task1',id)
        },
        onUpdate(id)
        {
            console.log('inside update task here1112',id)
            this.showUpdateTask = !this.showUpdateTask
            
            this.$emit('update-task1',id)
        },
    }
}

</script>
<style scope>
.fas {
    color: red;
    font-size: 28px;
}
.fa {
    color:rgb(19, 122, 169);
    margin-top: 3px;
}
.buttons {
    display: flex; /* Add flex container to the buttons */
}

.buttons i {    
    margin-right: 5px;
    /* Adjust the margin-right value as needed for your desired spacing */
    margin-left: 5px; 
    padding: 5px;
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