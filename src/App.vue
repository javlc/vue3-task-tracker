<template>
  <div class="container">
    <HeaderComp
      title="Task Tracker"
      :show-add-task="showAddTask"
      @toggle-add-task="toggleAddTask"
    />
    <router-view :show-add-task="showAddTask"></router-view>
    <FooterComp />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HeaderComp from '@/components/HeaderComp.vue'
import FooterComp from '@/components/FooterComp.vue'
export default defineComponent({
  name: 'App',
  components: {
    HeaderComp,
    FooterComp,
  },
  data() {
    return {
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
  },
})
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

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
