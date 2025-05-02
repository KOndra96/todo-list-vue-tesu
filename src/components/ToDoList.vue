<template>
    <section id="to-do-list">
        <h1>To-Do List made with Vue</h1>
        <AddNewTask />
        <ul>
            <li v-for="task in tasks" :key="task.id">
                <article>
                    <header>
                        <h2>{{ task.name }}</h2>
                        <button v-if="!task.editingTask" @click="editTask(task.id)">Edit</button>
                        <button v-else @click="editTask(task.id)">Done</button>


                        <button @click="removeTask(task.id)">Remove</button>
                    </header>
                    <p v-if="!task.editingTask">{{ task.description }}</p>
                    <textarea v-else v-model="task.newText" @keyup.enter="editTask(task.id)">{{ task.description }}</textarea>
                </article>
            </li>
        </ul>
    </section>
</template>
<script setup>
import { ref, onMounted } from 'vue';
import AddNewTask from './AddNewTask.vue';

const tasks = ref([]);

async function getTasks() {
    try {
        const response = await fetch('https://hp-api.onrender.com/api/spells');
        const data = await response.json();
        tasks.value = data;

        tasks.value.forEach(task => {
            task.editingTask = false;
            task.newText = task.description;
        });
    } catch (error) {
        console.error('Error fetching tasks: ', error);
        return [];
    }
}

function removeTask(id) {
    const index = tasks.value.findIndex((task) => task.id === id);
    if (index === -1) return console.error('Task not found');
    tasks.value.splice(index, 1);
}

function editTask(id) {
    const index = tasks.value.findIndex((task) => task.id === id);
    if (index === -1) return console.error('Task not found');

    const isEditing = tasks.value[index].editingTask;
    tasks.value[index].editingTask = !isEditing;

    if(isEditing) {
        tasks.value[index].description = tasks.value[index].newText;
    }

    // console.log(event);
    // if ()
}

onMounted(getTasks);

</script>
<style scoped lang="scss">
#to-do-list {
    max-width: 100%;

    padding-block: 1rem;
    padding-inline: 2rem;

    border-radius: .75rem;

    background-color: rgb(50, 50, 50);

    h1 {
        margin-bottom: .5rem;
        text-align: center;
    }

    ul {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 1rem;
        list-style-type: none;

        margin-top: 0;
        padding: 0;

        li {
            min-height: 10rem;

            padding: .75rem;

            border-radius: .5rem;

            background-color: rgba($color: #ffffff, $alpha: 0.15);

            article {
                display: flex;
                flex-direction: column;

                height: 100%;

                header {
                    display: flex;
                    justify-content: flex-end;
                    align-items: center;
                    gap: .5rem;

                    h2 {
                        margin-right: auto;
                        margin-bottom: .5rem;
                    }

                    button {
                        padding-block: .25rem;
                        padding-inline: .75rem;
                    }
                }

                p {
                    margin: 0;
                    margin-bottom: .5rem;
                }
            }

        }
    }
}

@media screen and (max-width: 600px) {
    #to-do-list {
        padding-inline: 5vw;

        ul {
            grid-template-columns: 1fr;
        }
    }
}
</style>