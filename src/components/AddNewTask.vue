<template>
    <form id="add-new-task" @submit.prevent="submitNewTask(newName, newDescription)">
        <div class="task-group" :class="{ error: errorName }">
            <label for="task-name">Task Name</label>
            <transition name="error-transition">
                <p v-if="errorName">{{ errorNameText }}</p>
            </transition>
            <input type="text" id="task-name" placeholder="Type here..." v-model="newName">
        </div>

        <div class="task-group" :class="{ error: errorDescription }">
            <label for="task-description">Task Description</label>
            <transition name="error-transition">
                <p v-if="errorDescription">{{ errorDescriptionText }}</p>
            </transition>
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

const errorName = ref(false);
const errorNameText = ref('');

const errorDescription = ref(false);
const errorDescriptionText = ref('');

function submitNewTask(name, description) {
    if (!name) {
        hideErrors();
        showNameError('Please enter a task name');
        return;
    }
    if (!description) {
        hideErrors();
        showDescriptionError('Please enter a description');
        return;
    }

    hideErrors();
    emit('add-new-task', name, description);
}

//add showing errors
function showNameError(error) {
    errorNameText.value = error;
    errorName.value = true;
}

function showDescriptionError(error) {
    errorDescriptionText.value = error;
    errorDescription.value = true;
}

function hideNameError() {
    errorName.value = false;
}

function hideDescriptionError() {
    errorDescription.value = false;
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

        p {
            margin: 0;
            margin-bottom: .25rem;

            font-style: italic;
            font-weight: 700;
            color: red;
        }

        &.error {
            input {
                outline: none;
                border: .125rem solid red;
            }
        }
    }
}

.error-transition-enter-active,
.error-transition-leave-active {
    transition: opacity 0.5s ease, transform 0.5s ease;
}

.error-transition-enter-from,
.error-transition-leave-to {
    opacity: 0;
    transform: translateY(-1rem);
}

@media screen and (max-width: 600px) {
    #add-new-task {
        grid-template-columns: 1fr;
    }
}
</style>