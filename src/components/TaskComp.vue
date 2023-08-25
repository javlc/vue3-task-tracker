<template>
  <div
    :class="[task.reminder ? 'reminder' : '', 'task']"
    @dblclick="$emit('toggle-reminder', task.id)"
  >
    <h3>
      {{ task.text }}
      <XmarkIcon @click="$emit('delete-task', task.id)" />
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue'
import XmarkIcon from './icons/XmarkIcon.vue'
export default defineComponent({
  name: 'TaskComp',
  components: {
    XmarkIcon,
  },
  props: {
    task: {
      type: Object,
      default: () => {},
    },
  },
  emits: ['toggle-reminder', 'delete-task'],
})
</script>
<style scoped>
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.task h3 svg {
  fill: red;
}
</style>
