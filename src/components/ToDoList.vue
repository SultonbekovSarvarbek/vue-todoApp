<template>
  <div>
    <ul>
      <ToDoItem
        v-for="(todo,i) in todos"
        v-bind:todo="todo"
        v-bind:key="todo.id"
        v-on:remove-ToDo="removeToDo"
        v-bind:index="i"
      ></ToDoItem>
    </ul>
  </div>
</template>

<script>
import ToDoItem from "@/components/ToDoItem";
export default {
  props: ["todos"],

  components: {
    ToDoItem
  },
  methods: {
    removeToDo(id) {
      this.$emit("remove-ToDo", id);
    }
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>