<template>
    <section id="to-do-list">
        <h1>To-Do List made with Vue</h1>
        <AddNewTask />
        <ul>
            <li>
                <article>
                    <h2>Lorem Lorem Lorem</h2>
                    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Optio voluptates ratione exercitationem
                        numquam itaque, porro nisi deserunt eveniet aliquid consequuntur rerum non et voluptas, debitis
                        iure
                        inventore! Quo, nihil. Quisquam.</p>
                </article>
            </li>
            <li>
                <article>
                    <h2>Lorem Lorem Lorem</h2>
                    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Iure laborum quo eveniet fugit expedita
                        suscipit voluptates architecto! Ut inventore eveniet culpa nostrum, corrupti delectus
                        perspiciatis
                        modi hic quia distinctio cupiditate omnis, ullam, magni sit porro minus numquam aut! Nemo sunt
                        et
                        adipisci quibusdam numquam explicabo ea, doloremque, soluta ducimus quis, dolorum eaque odit
                        assumenda rem quod mollitia earum amet obcaecati debitis facilis tempora officiis eius? Quasi
                        eum
                        ullam magni, voluptas veniam sed. Repellat architecto reiciendis aperiam quaerat molestias iusto
                        odio omnis rem amet excepturi ducimus nesciunt, voluptate quas id aspernatur. Vero vel
                        exercitationem distinctio iusto eveniet necessitatibus harum velit aspernatur maxime, eos
                        consequatur voluptates, explicabo accusamus nostrum veritatis doloremque, illo odit voluptas
                        blanditiis dolor odio ab quas corporis. Porro sunt, modi enim reprehenderit ducimus possimus
                        provident rem dolorum architecto fuga nemo nesciunt dolores accusamus et similique deserunt
                        voluptas
                        eaque? Libero nesciunt consequatur cupiditate maxime suscipit sint praesentium voluptate
                        quibusdam
                        aliquam eaque amet ea, tempore voluptatibus quisquam nisi? Deserunt consectetur eos animi
                        necessitatibus rerum incidunt iure voluptate repellendus consequuntur, illum ratione natus,
                        molestiae tempora tenetur voluptatum dolorum eaque quidem doloribus? Magnam eius, labore
                        adipisci
                        laudantium eligendi esse quae vero quisquam quod ab saepe facilis. Sapiente vel temporibus dicta
                        architecto iusto quae tempore inventore qui numquam facere! Non, sint magni optio incidunt
                        consequatur esse officiis asperiores iusto hic tempore. Blanditiis aspernatur inventore ratione
                        voluptas ipsa debitis vel? Quasi quo libero accusantium iure laboriosam quas officia explicabo
                        dolor, qui facilis a, temporibus, modi delectus expedita! Molestiae sequi temporibus nisi cum
                        dolorem. Praesentium, architecto!</p>
                </article>
            </li>
        </ul>
    </section>
</template>
<script setup>
import AddNewTask from './AddNewTask.vue';
</script>
<style scoped lang="scss">
#to-do-list {
    max-width: 100%;

    padding: 2rem;

    border-radius: .75rem;

    background-color: rgb(50, 50, 50);

    h1 {
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
            padding: .75rem;

            border-radius: .5rem;

            background-color: rgba($color: #ffffff, $alpha: 0.15);

            article {
                h2 {
                    margin-bottom: .5rem;
                }
                p {
                    margin: 0;
                }
            }

        }
    }
}

@media screen and (max-width: 600px) {
    #to-do-list {
        padding-inline: 5vw;
    }
}
</style>