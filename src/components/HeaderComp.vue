<template>
  <header>
    <h1>{{ title }}</h1>
    <ButtonComp
      v-show="isHomePage"
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'green'"
      @btn-click="$emit('toggle-add-task')"
    />
  </header>
</template>

<script>
import ButtonComp from './ButtonComp.vue';
export default {
  name: 'HeaderComp',
  components: {
    ButtonComp,
  },
  props: {
    title: {
      type: String,
      default: () => '',
    },
    showAddTask: Boolean,
  },
  emits: ['toggle-add-task'],
  computed: {
    isHomePage() {
      if (this.$route.path === '/') {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
