<template>
    <div>
        <p class="info-task">Title</p>
        <h3 class="task-title" :class="task.is_complete ? 'task-complete' : ''">{{ task.title }}</h3>
        <p class="info-task">Number Task</p>
        <h3 class="task-title">{{ task.id }}</h3>
        <p class="info-task">Task Description</p>
        <h5 class="task-description">{{ task.description }}</h5>
        <template v-if="showInputs">
            <form class="form-tasks" @submit.prevent="editTask">
                <input class="input-title" type="text" v-model="title">
                <input class="input-description-task" type="text" v-model="description">
                <button class="button-update" type="submit">Update</button>
            </form>
        </template>
        <div class="buttons-edit-container">
            <button class="buttons-change" @click="showEditTask">Edit</button>
            <button class="buttons-change-complete" @click="completeTask">{{
                task.is_complete ? "UnDone" : "Done"
            }}</button>
            <button class="button-delete" @click="deleteTask">Delete</button>
        </div>
        <div class="img-buttons-container">
            <img class="edit-img"
                src="https://res.cloudinary.com/dn73thusg/image/upload/v1674133401/Final-Project/edit_image_ijkquj.jpg"
                alt="edit_img">
            <img class="done-img"
                src="https://res.cloudinary.com/dn73thusg/image/upload/v1674553400/Final-Project/done_buttom_1_qaxvjg.png"
                alt="done_button">
            <img class="delete-img"
                src="https://res.cloudinary.com/dn73thusg/image/upload/v1674553317/Final-Project/delete_button_izakyo.jpg"
                alt="delete_button">
        </div>
    </div>

</template>

<script setup>
import { ref } from 'vue';
import { useTaskStore } from '../stores/task';
import { supabase } from '../supabase';


const taskStore = useTaskStore();
//--------------------------
let title = ref("");
let description = ref("");

const showInputs = ref(false);

const name = ref("");
const emit = defineEmits(["childEdit", "childDone", "childDelete"]);
//--------------------------
const props = defineProps(["task"]);
/// ------------------------
const done = ref(false)

// Función para borrar la tarea a través de la store. El problema que tendremos aquí (y en NewTask.vue) es que cuando modifiquemos la base de datos los cambios no se verán reflejados en el v-for de Home.vue porque no estamos modificando la variable tasks guardada en Home. Usad el emit para cambiar esto y evitar ningún page refresh.
//--------------------------------------------

const showEditTask = () => {
    showInputs.value = !showInputs.value
    title.value = props.task.title;
    description.value = props.task.description;
};

// FALTA ACABAR EDIT

const editTask = () => {
    console.log(props.task.title);
    console.log(props.task.description);

    if (title.length === 0) {
        console.log("el titulo esta vacio, porfavor introduce titulo");
    } else {

        console.log("hola mundo");
        let newTaskDescription = {
            id: props.task.id,
            title: title.value,
            description: description.value
        };
        emit("childEdit", newTaskDescription);
        showInputs.value = !showInputs.value
    }
}
// funcion que se enarga de recibir una funcion desde el padre mediante un EMIT que es una manera de vue de poder implementar esta logica, basicamente una ayuda para pasar logica entre componente 
const completeTask = () => {
    emit("childDone", props.task)
    //  console.log(props.task);
}

const deleteTask = () => {
    //await taskStore.deleteTask(props.task.id);
    emit("childDelete", props.task.id);
};
//------------------------------------------------
</script>

<style>
/*
.task-title {
    padding: 0 100px;
    margin: 20px;
    border: 1px solid #1d1919;
    border-radius: 10px;
    background-color: #1d1919;
    color: #c3bcbc;
}

.task-description {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin: 20px;
    padding: 25px;
    border: 1px solid #1d1919;
    border-radius: 10px;
    background-color: #1d1919;
    color: #c3bcbc;
}

.task-complete {
    text-decoration: line-through;
    color: #e94d4d;
}

.flex-container {
    display: flex;
    flex-direction: initial;
    justify-content: space-evenly;
    align-items: baseline;
}*/
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
