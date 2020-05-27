<template>
    <form @submit.prevent="onSubmit">
        <input v-model="title" type="text">
        <button type="submit" class="btn__add">Add</button>
    </form>
</template>


<script>
    export default {
        data: function () {
            return {
                title: ''

            }
        },
        methods: {
            onSubmit() {
                if (this.title.trim()) {
                    const newTodo = {
                        id: Date.now(),
                        title: this.title,
                        date: new Date().toLocaleString(),
                        completed: false
                    }
                    this.$emit('add-todo', newTodo)
                    this.title = ''

                }
            }
        }
    }
</script>

<style scoped>
    input {
        border: 1px solid #333;
        padding: 0.2rem;
    }

    .btn__add {
        background-color: rgb(7, 186, 63);
        border: none;
        margin-left: 20px;
        border-radius: 7px;
        padding: .5rem 1rem;
        cursor: pointer;
    }
</style>