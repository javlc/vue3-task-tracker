<template>
  <div class="home">
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks
      :tasks="tasks"
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
    />
  </div>
</template>

<script>
import AddTask from '../components/AddTask.vue';
import TasksComp from '../components/TasksComp.vue';

export default {
  name: 'HomeView',
  components: {
    Tasks: TasksComp,
    AddTask,
  },
  props: {
    showAddTask: Boolean,
  },
  data() {
    return {
      tasks: [],
    };
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
  methods: {
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(task),
      });

      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        });

        res.status === 200
          ? (this.tasks = this.tasks.filter((item) => item.id !== id))
          : alert('Error deleting task');
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);
      const updTask = await {
        ...taskToToggle,
        reminder: !taskToToggle.reminder,
      };
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(updTask),
      });
      const data = await res.json();

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task,
      );
    },
    async fetchTasks() {
      const res = await fetch('api/tasks');
      const data = await res.json();

      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();

      return data;
    },
  },
};
</script>
