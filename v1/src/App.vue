<template>
  <v-app id="app">
    <v-app-bar
      color="grey lighten-5"
      max-height="120"
      height="120"
      elevation="8"
    >
      <v-img
        position="49% -10px"
        height="255"
        contain
        src="./assets/PinIt.png"
      ></v-img>
    </v-app-bar>
    <v-content>
      <v-container class="py-0">
        <v-card
          class="mx-auto mb-10"
          min-
          max-width="1200"
          min-height="720"
          elevation="8"
          id="cork"
        >
          <v-card class="py-2 white--text" color="indigo lighten-1" tile>
            <h2 class="headline">
              Completed Tasks:
              {{
                todos.filter(todo => {
                  return todo.done === true;
                }).length
              }}
            </h2>
            <h2 class="headline">
              Pending Tasks:
              {{
                todos.filter(todo => {
                  return todo.done === false;
                }).length
              }}
            </h2>
          </v-card>
          <CreateTodo class="mt-2" @add-todo="addTodo" />
          <TodoList
            class="py-0"
            @complete-todo="completeTodo"
            @pending-todo="pendingTodo"
            :todos="todos"
          />
        </v-card>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import TodoList from "./components/TodoList";
import CreateTodo from "./components/CreateTodo";

export default {
  name: "App",
  components: {
    TodoList,
    CreateTodo
  },
  data() {
    return {
      todos: [
        {
          name: "Me",
          task: "Write my first to-do!",
          done: false
        }
      ]
    };
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo);
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
    },
    pendingTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = false;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #ede7f6;
}
#cork {
  background-image: url("./assets/cork.jpg");
  background-repeat: repeat;
}
</style>
