<template>
    <form id="add-new-task" @submit.prevent="submitNewTask(newName, newDescription)">
        <div class="task-group">
            <label for="task-name">Task Name</label>
            <input type="text" id="task-name" placeholder="Type here..." v-model="newName">
        </div>

        <div class="task-group">
            <label for="task-description">Task Description</label>
            <input type="text" id="task-description" placeholder="Type here..." v-model="newDescription">
        </div>

        <button type="submit">Add New Task</button>
    </form>
</template>
<script setup>
import { ref, defineEmits } from 'vue';

const emit = defineEmits(['add-new-task', 'empty-name', 'empty-description']);

const newName = ref('');
const newDescription = ref('');

function submitNewTask(name, description) {
    if (!name) return showNameError('Please enter a task name');
    if (!description) return showDescriptionError('Please enter a description');

    hideErrors();
    emit('add-new-task', name, description);
}

//add showing errors
function showNameError(error) {

}

function showDescriptionError(error) {
    
}

function hideNameError() {

}

function hideDescriptionError() {
    
}

function hideErrors() {
    hideNameError();
    hideDescriptionError();
}
</script>
<style scoped lang="scss">
#add-new-task {
    display: grid;
    grid-template-columns: repeat(2, 2fr) 1fr;
    align-items: end;
    gap: 1rem;

    width: 100%;

    margin-bottom: 1rem;

    label {
        margin-bottom: .25rem;
    }

    input,
    button {
        padding: .5rem;

        border: none;
        border-radius: .5rem;

        font-size: .8rem;

        background-color: #f9f9f9;
        color: rgb(20, 20, 20);

        transition: color .15s ease, background-color .15s ease;

        &:focus,
        &:hover {
            background-color: #d4d4d4;
            color: black;
        }
    }

    input {
        &::placeholder {
            font-size: .8rem;
            color: rgb(20, 20, 20);
        }
    }

    button {
        cursor: pointer;
    }

    .task-group {
        display: flex;
        flex-direction: column;
    }
}

@media screen and (max-width: 600px) {
    #add-new-task {
        grid-template-columns: 1fr;
    }
}
</style>