<template>
    <div class="card bg-dark text-light border-2 text-center m-4">
    <div class="card-body p-4">
      <h4 class="card-title" :class="{ taskComplete: task.is_complete }">{{ task.title }}</h4>
      <p class="card-text" :class="{ taskComplete: task.is_complete }">{{ task.description }}</p>
      <button class="btn btn-danger m-1 " @click="deleteTask">Delete</button>
      <button class="btn btn-success m-1" @click="toggleComplete">Done</button>
      <button class="btn btn-primary m-1" @click="updateToggle">Edit</button>
      <div v-if="inputUpdate">
        <input class="m-2" type="text" :placeholder="task.title" v-model="name" />
        <input class="m-2" type="text" :placeholder="task.description" v-model="description" />
        <button class="btn btn-primary" @click="updateTask">Update</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onUpdated, watch } from "vue";
import { useTaskStore } from "../stores/task";
import { supabase } from "../supabase";

const taskStore = useTaskStore();
const name = ref("");
const description = ref("");
const props = defineProps({
  task: Object,
});

// Función para borrar la tarea a través de la store. El problema que tendremos aquí (y en NewTask.vue) es que cuando modifiquemos la base de datos los cambios no se verán reflejados en el v-for de Home.vue porque no estamos modificando la variable tasks guardada en Home. Usad el emit para cambiar esto y evitar ningún page refresh.
const deleteTask = async () => {
  await taskStore.deleteTask(props.task.id);
};

// variable inputUpdate la utilizo en false para luego utilizarla en el dom para mantener ocultos los inputs para hacer un update
const inputUpdate = ref(false);

// funcion basica para hacer un toggle a traves de un boton @click para cambiar la variable inputUpdate de false a true y con esto dejar ver en el DOM dichos inputs y el boton para hacerel update
const updateToggle = () => {
  inputUpdate.value = !inputUpdate.value;
};

// funcion que llama a funcion de la store task.js que se encarga de hacer una actualizacion de los datos de la tarea.
const updateTask = () => {
  taskStore.updateTask(props.task.id, name.value, description.value);
  name.value = "";
  description.value = "";
  updateToggle();
};

const toggleComplete = () => {
  props.task.is_complete = !props.task.is_complete;
  taskStore.completeTask(props.task.id, props.task.is_complete);
};
</script>

<style>
.taskComplete {
  text-decoration: line-through;
}
</style>

<!--
**Hints**
1. ref() or reactive() can be used here to store the following, think if you want to store them either individually or
like an object, up to you.

2. Data properties need here are the following: a boolean to store a false**Important variable, a string to store an error,
a string to store the value of the task that the user can edit, an initial false boolean to hide the inputFIeld used to edit
the new task detail or details[this is in reference of the task title and the task description].

3. Store the custom emit events that will be used to call the functions of the homeView for editing, deleting and toggling the
status[completed, not complted] of the taskItem.

4. Function to handle the error with the data properties used to control the error and the the boolean controlling the boolean
empty variable.

5. Function to handle the edit dialogue where the inputField is displayed and the string used to store the value of the
inputField will be used here to save the value as a prop on this function.

6. Function to emmit a custom event emit() that takes 2 parameters a name for the custom event and the value that will be
send via the prop to the parent component. This function can control the toggle completion of the task on the homeview.

7. Function to edit the task information that you decided that the user can edit. This function's body takes in a conditional
that first checks if the value of the task [either title and description or just title] is empty which if true it runs the
function used to handle the error on hint4. Else, the conditional sets the first mentioned boolean data property on hint2
back to its inital boolean value to hide the error message and repeat the same for the data property mentioned 4th on hint2;
a constant that stores an object that holds the oldValue from the prop item and the value of the task coming from the data
property mentioned 3rd on hint2; a custom event emit() that takes 2 parameters a name for the custom event and the value
from the object used on this part of the conditional and lastly this part of the conditional sets the value of input field
to an empty string to clear it from the ui.

8. Function to emmit a custom event emit() that takes 2 parameters a name for the custom event and the value that will be
send via the prop to the parent component. This function can control the removal of  the task on the homeview.
-->
