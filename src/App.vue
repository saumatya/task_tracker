<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" @toggle-update-task="toggleUpdateTask" 
            title="Task Tracker" 
            :showAddTask = "showAddTask"
            :showUpdateTask = "showUpdateTask"/>
    <div v-show="showAddTask" >
      <AddTask @add-task="addTask"/>
    </div> 
    <div v-show="showUpdateTask" >
      <UpdateTask @update-task="updateTask"/>
    </div> 
    <Tasks @toggle-update-task="toggleUpdateTask" 
    @toggle-reminder="toggleReminder" 
    @delete-task2="deleteTask" 
    @update-task2="updateTask" :tasksInside="tasks"/>
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'
import UpdateTask from './components/UpdateTask'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
    UpdateTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
      showUpdateTask:false
    }
  },
  methods: {
    toggleAddTask(){
      console.log('toggleAddTask')
      this.showAddTask = !this.showAddTask
    },
    toggleUpdateTask(){
      console.log('toggleUpdateTask')
      this.showUpdateTask = !this.showUpdateTask
    },
    async addTask(task){
      console.log('olen tä')
      const res = await fetch('api/tasks',{
        method: 'POST',
        headers: {
          'Content-type':'application/json',
        },
        body: JSON.stringify(task)
      })
 
      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },
    async toggleReminder(id)
    {
      console.log('inside app toggle reminder', id)
      // futher reading

      const taskToToggle = await this.fetchTaskById(id)
      const updateTask = {...taskToToggle, reminder : !taskToToggle.reminder}

      const res = await fetch (`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updateTask)
      })

      const data = await res.json()

      this.tasks = this.tasks.map((task) => 
      task.id === id ? { ...task, reminder : data.reminder} :task
      )
    },
    async updateTask(id)
    {
      console.log('App som ting wong',id)
      const res = await(fetch(`api/tasks/${id}`))
      const data = await res.json()
      console.log(data)
      return data
    },
    async deleteTask(id)
    {
      console.log('inside app',id)
      if (confirm('Are you sure?'))
      {
        const res = await fetch(`api/tasks/${id}`,{
          method: 'DELETE',
        })

        res.status === 200 ?(this.tasks = this.tasks.filter((task) => task.id !== id)): alert('Error deleting task')


      // further reading
      // this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    async fetchTasks() {
      const res = await(fetch('api/tasks'))
      const data = await res.json()
      return data
    },
    async fetchTaskById(id)
    {
      const res = await(fetch(`api/tasks/${id}`))
      const data = await res.json()
      return data
    }
  },
  async created ()
  {
    this.tasks = await this.fetchTasks()
  }
}
</script>

<!-- <style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style> -->
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
