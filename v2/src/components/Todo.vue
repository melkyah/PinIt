<template>
  <v-container>
    <v-card
      elevation="16"
      class="mx-auto animated fadeIn faster"
      min-height="290"
      max-width="300"
      color="yellow lighten-4"
    >
      <v-card-title id="title" class="mx-auto py-1">
        <h2 class="headline mx-auto">{{ todo.name }}</h2>
      </v-card-title>
      <v-card-subtitle id="subtitle" class="my-1 py-1">
        <h2 class="subtitle mx-auto">{{ todo.task }}</h2>
      </v-card-subtitle>
      <v-row
        id="icons"
        class="mx-0 pr-2"
        justify="end"
        align="end"
        v-show="!isEditing"
      >
        <v-icon id="edit-icon" @click="showForm"
          >mdi-square-edit-outline
        </v-icon>
        <v-icon id="trash-icon" @click="deleteTodo(todo)"
          >mdi-trash-can-outline
        </v-icon>
      </v-row>
      <v-card
        color="yellow lighten-5"
        id="edit"
        outlined
        class="my-2 py-2 mx-6 px-2"
        v-show="isEditing"
      >
        <v-form>
          <v-text-field label="Name" v-model="todo.name" />
          <v-text-field label="Task" v-model="todo.task" />
          <v-btn color="blue darken-1" @click="hideForm">
            <p class="title font-weight-bold my-auto white--text">Close X</p>
          </v-btn>
        </v-form>
      </v-card>
      <v-row align="end" id="completed" v-show="!isEditing && todo.done">
        <v-col class="py-0">
          <v-btn
            tile
            block
            depressed
            color="green darken-1"
            @click="pendingTodo(todo)"
          >
            <p class="my-0 font-weight-bold white--text">Completed</p>
          </v-btn>
        </v-col>
      </v-row>
      <v-row align="end" id="pending" v-show="!isEditing && !todo.done">
        <v-col class="py-0">
          <v-btn
            tile
            block
            depressed
            color="red darken-1"
            @click="completeTodo(todo)"
          >
            <p class="my-0 font-weight-bold white--text">Pending</p>
          </v-btn>
        </v-col>
      </v-row>
    </v-card>
  </v-container>
</template>

<script>
export default {
  props: ["todo"],
  data() {
    return {
      isEditing: false
    };
  },
  methods: {
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
    deleteTodo(todo) {
      this.$emit("delete-todo", todo);
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

<style>
#title {
  background-color: #fffde7;
}
#icons {
  height: 160px;
}
#completed {
  height: 40px;
}
#pending {
  height: 40px;
}
</style>
