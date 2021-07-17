<template>
  <Header title="Task Tracker" />
  <Tasks @delete-task="deleteTask" :tasks="tasks" />
</template>

<script>
import Header from './components/Header';
import Tasks from './components/Tasks';

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
    deleteTask(id) {
      console.log('task', id);
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
