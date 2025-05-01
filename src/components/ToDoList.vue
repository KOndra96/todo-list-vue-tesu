<template>
    <section id="to-do-list">
        <h1>To-Do List made with Vue</h1>
        <AddNewTask />
        <ul>
            <li v-for="task in tasks" :key="task.id">
                <article>
                    <header>
                        <h2>{{ task.name }}</h2>
                        <button @click="removeTask(task.id)">Remove</button>
                    </header>
                    <p>{{ task.description }}</p>
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
    } catch (error) {
        console.error('Error fetching tasks: ', error);
        return [];
    }
}

function removeTask(id) {
    const index = tasks.value.findIndex((task) => task.id === id);
    if (index !== -1) {
        tasks.value.splice(index, 1);
    }
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
                    justify-content: space-between;
                    align-items: center;

                    h2 {
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