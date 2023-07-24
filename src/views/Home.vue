<template>
  <Nav />
  <div class="container text-center">
    <NewTask/>
    <h2 class="fw-bold m-5">My Tasks</h2>
    <TaskItem v-for="task in tasks" :key="task.id" :task="task" />
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import { useTaskStore } from "../stores/task";
import Nav from '../components/Nav.vue';
import NewTask from '../components/NewTask.vue';
import TaskItem from '../components/TaskItem.vue';

import Swal from 'sweetalert2';

const taskStore = useTaskStore();

const tasks = computed(() => taskStore.tasksArr);
// console.log("taskComputed:", tasks.value);



onMounted(async () => {
  await taskStore.fetchTasks();
  // console.log("taskOnmouted:", tasks.value);
});


</script>


<style></style>