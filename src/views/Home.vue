<template>
  <Nav />
  <div class="container text-center">
    <NewTask/>
    <h2 class="fw-bold m-5">My Tasks</h2>
    <div class="grid-container">
      <TaskItem v-for="task in tasks" :key="task.id" :task="task" />
    </div>
  </div>
  <Footer />
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import { useTaskStore } from "../stores/task";
import Nav from '../components/Nav.vue';
import NewTask from '../components/NewTask.vue';
import TaskItem from '../components/TaskItem.vue';
import Swal from 'sweetalert2';
import Footer from '../components/Footer.vue';

const taskStore = useTaskStore();

const tasks = computed(() => taskStore.tasksArr);
// console.log("taskComputed:", tasks.value);



onMounted(async () => {
  await taskStore.fetchTasks();
  // console.log("taskOnmouted:", tasks.value);
});


</script>


<style>
.grid-container {
  justify-content: space-around;
  display: grid;
  grid-template-columns: repeat(auto-fill, 340px);
  grid-auto-rows: auto;
  grid-gap: 5px;
}
</style>