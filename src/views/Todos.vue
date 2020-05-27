<template>
    <div>
        <router-link to="/">Home</router-link>

        <hr />
        <select v-model="filter">
            <option value="all">all</option>
            <option value="completed">completed</option>
            <option value="not-completed">not-completed</option>
        </select>

        <AddToDo @add-todo="addtodo" />


        <Loader v-if="loading"></Loader>

        <ToDoList v-else-if="filteredTodos.length" v-bind:todos="filteredTodos" @remove-ToDo="removeToDo" />
        <p v-else>No todos</p>


    </div>
</template>

<script>
    import ToDoList from "@/components/ToDoList";
    import AddToDo from "@/components/AddToDo";
    import Loader from "@/components/Loader";
    export default {
        name: "App",
        data() {
            return {
                todos: [],
                loading: true,
                filter: 'all',

            };
        },
        mounted() {
            fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
                .then(response => response.json())
                .then(json => {
                    setTimeout(() => {
                        this.loading = false
                        this.todos = json

                    }, 3000)

                })
        },
        components: {
            ToDoList,
            AddToDo,
            Loader
        },
        computed: {
            filteredTodos() {
                if (this.filter === 'all') {


                    return this.todos

                }
                if (this.filter === 'completed') {

                    return this.todos.filter(t => t.completed)


                }
                if (this.filter === 'not-completed') {

                    return this.todos.filter(t => !t.completed)


                }

            }
        },
        methods: {
            removeToDo(id) {
                this.todos = this.todos.filter(t => t.id !== id);
            },
            addtodo(todo) {
                this.todos.push(todo);
            }
        }
    };
</script>