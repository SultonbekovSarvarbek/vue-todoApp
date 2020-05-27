<template>
  <li>
    <div class="todo">
      <div class="todo__date">{{ todo.date }}</div>
      <div>
        <span v-bind:class="{done: todo.completed }">
          <input type="checkbox" v-on:change="todo.completed=!todo.completed " />
          <strong>{{ index + 1 }}</strong>
          {{ todo.title | uppercase }}
        </span>
        <button v-on:click="$emit('remove-ToDo',todo.id)">&times;</button>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase();
    }
  }
};
</script>

<style scoped>
li {
  border: 2px solid #333;
  padding: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px 0;
}

.todo {
  display: flex;
  flex-direction: column;
}

.todo__date {
  display: block;
  margin-bottom: 0.4rem;
}

button {
  background-color: red;
  border: none;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  cursor: pointer;
  font-weight: bold;
}

span,
input {
  margin-right: 20px;
}

.done {
  text-decoration: line-through;
}
</style>