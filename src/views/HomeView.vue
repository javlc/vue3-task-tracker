<template>
  <div class="home">
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks :tasks="tasks" @toggle-reminder="toggleReminder" @delete-task="deleteTask" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import AddTask from '../components/AddTask.vue'
import TasksComp from '../components/TasksComp.vue'
import type { Task } from '@/types/TaskTrackerTypes'

export default defineComponent({
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
      tasks: [] as Task[],
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
  },
  methods: {
    async addTask(task: Task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(task),
      })

      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },
    async deleteTask(id: number) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })

        res.status === 200
          ? (this.tasks = this.tasks.filter((item) => item.id !== id))
          : alert('Error deleting task')
      }
    },
    async toggleReminder(id: number) {
      const taskToToggle = await this.fetchTask(id)
      const updTask = await {
        ...taskToToggle,
        reminder: !taskToToggle.reminder,
      }
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(updTask),
      })
      const data = await res.json()

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task,
      )
    },
    async fetchTasks() {
      const res = await fetch('api/tasks')
      const data = await res.json()

      return data
    },
    async fetchTask(id: number) {
      const res = await fetch(`api/tasks/${id}`)
      const data = await res.json()

      return data
    },
  },
})
</script>
