<template>
  <Header title="Task Tracker" :showAddTask="showAddTask" @toggle-add-task="toggleAddTask" />
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
    async deleteTask(id) {
      if(confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE'
        });

        res.status === 200 ? (this.tasks = this.tasks.filter(task => task.id !== id)) : alert('Error deleting the task');
      }
    },
    async toggleReminder(id) {
      const taskToChange = await this.fetchTask(id);
      
      const updatedTask = { ...taskToChange, reminder: !taskToChange.reminder }

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updatedTask)
      });

      const data = await res.json();

      res.status===200 ? (this.tasks = this.tasks.map(task => task.id===id ? { ...task, reminder: data.reminder } : { ...task } )) : alert('Failed to update reminder status');
    },
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(task)
      });

      const data = await res.json();
      
      this.tasks = [...this.tasks, data];
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      // const res = await fetch(`api/tasks/${id}`);
      // const data = await res.json();
      const data = await this.tasks.find(ele => ele.id === id);

      return data;
    }
  },
  async created() {
    // Created is the lifecycle method for api calls
    this.tasks = await this.fetchTasks();
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
