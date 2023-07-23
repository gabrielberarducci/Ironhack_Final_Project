<template>
  <Nav />
  <div class="container text-center">
    <div class="content">
      <p class="date">{{ fechaFormateada }}</p>
    </div>
    <NewTask/>
    <h2 class="title">My Tasks</h2>
    <TaskItem v-for="task in tasks" :key="task.id" :task="task" />
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import { useTaskStore } from "../stores/task";
import Nav from '../components/Nav.vue';
import NewTask from '../components/NewTask.vue';
import TaskItem from '../components/TaskItem.vue';
import { format } from 'date-fns';
import Swal from 'sweetalert2';

const taskStore = useTaskStore();

const tasks = computed(() => taskStore.tasksArr);
// console.log("taskComputed:", tasks.value);

const fechaFormateada = ref('');

onMounted(async () => {
  await taskStore.fetchTasks();
  // console.log("taskOnmouted:", tasks.value);

  // Obtener la fecha actual
  const fecha = new Date();

  // Formatear la fecha en el formato deseado (por ejemplo, "8th July 2023")
  const formatoFecha = format(fecha, "dd MMMM yyyy  -  HH:mm");

  // Asignar la fecha formateada a la variable fechaFormateada
  fechaFormateada.value = formatoFecha;
  
});


</script>


<style>
.date {
  font-size: 2.5rem;
  font-weight: 900;
  text-align: center;
  
}
</style>