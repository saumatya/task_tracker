<template>
  <div class="container">
    <Header title="Task Tracker"/>
    <Tasks @toggle-reminder="toggleReminder" @delete-task2="deleteTask" :tasksInside="tasks"/>
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
export default {
  name: 'App',
  components: {
    Header,
    Tasks
  },
  data() {
    return {
      tasks: []
    }
  },
  methods: {
    toggleReminder(id)
    {
      console.log('inside app toggle reminder', id)
      // futher reading
      this.tasks = this.tasks.map((task) => 
      task.id === id ? { ...task, reminder : !task.reminder} :task
      )
    },
    deleteTask(id)
    {
      console.log('inside app',id)
      // futher reading
      this.tasks = this.tasks.filter((task) => task.id !== id)
    }
  },
  created ()
  {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors appointment',
        day: 'March 1st at 2:30 pm',
        reminder: true,
      },
      {
        id: 2,
        text: 'Meeting at school',
        day: 'August 21st at 10:00 am',
        reminder: false,
      },
      {
        id: 3,
        text: 'Sleepover with girlfriend',
        day: 'October 25th at 8:30 pm',
        reminder: true,
      },
    ]
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
