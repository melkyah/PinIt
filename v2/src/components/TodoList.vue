<template>
  <v-container fluid>
    <v-row>
      <v-col class="py-0">
        <Todo
          @delete-todo="deleteTodo"
          @complete-todo="completeTodo"
          @pending-todo="pendingTodo"
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
        ></Todo>
      </v-col>
    </v-row>
  </v-container>
</template>

<script type="text/javascript">
import Todo from "./Todo";

export default {
  props: ["todos"],
  components: {
    Todo
  },
  methods: {
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    completeTodo(todo) {
      this.$emit("complete-todo", todo);
    },
    pendingTodo(todo) {
      this.$emit("pending-todo", todo);
    }
  }
};
</script>
<style></style>
