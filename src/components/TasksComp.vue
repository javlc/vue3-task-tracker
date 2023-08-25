<template>
  <div v-for="task in tasks" :key="task.id">
    <TaskComp
      :task="task"
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @delete-task="$emit('delete-task', task.id)"
    />
  </div>
</template>
<script>
import TaskComp from './TaskComp.vue'
export default {
  name: 'TasksComp',
  components: {
    TaskComp,
  },
  props: {
    tasks: {
      type: Array,
      default: () => [],
    },
  },
  emits: ['delete-task', 'toggle-reminder'],
}
</script>
