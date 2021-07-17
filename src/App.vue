<template>
  <Header title="Task Tracker" @toggle-add-task="toggleAddTask" />
  <div v-if="showAddTask">
    <AddTask @add-task="addTask" />
  </div>
  <Tasks @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks" />
</template>

<script>
import Header from './components/Header';
import AddTask from './components/AddTask';
import Tasks from './components/Tasks';

export default {
  name: 'App',
  components: {
    Header,
    AddTask,
    Tasks
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    deleteTask(id) {
      if(confirm('Are you sure?')) {
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map(task => task.id===id ? { ...task, reminder: !task.reminder } : { ...task } );
    },
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    }
  },
  created() {
    // Created is the lifecycle method for api calls
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'March 1st at 2.30pm',
        reminder: true
      },
      {
        id: 2,
        text: 'Meeting at School',
        day: 'March 2nd at 2.30pm',
        reminder: false
      },
      {
        id: 3,
        text: 'Go Shopping',
        day: 'March 3rd at 2.30pm',
        reminder: true
      },
      {
        id: 4,
        text: 'Kill The Kids',
        day: 'March 4th at 2.30pm',
        reminder: false
      },
    ]
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
