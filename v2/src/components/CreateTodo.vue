<template>
  <v-container>
    <transition
      name="createButton"
      enter-active-class="animated fadeInDown faster"
      leave-active-class="animated fadeOutUp faster"
    >
      <v-btn
        elevation="12"
        class="animated fadeIn faster"
        fab
        color="blue darken-1"
        @click="openForm"
        v-show="!isCreating"
      >
        <v-icon color="white">mdi-tooltip-plus-outline</v-icon>
      </v-btn>
    </transition>
    <transition
      name="createCard"
      enter-active-class="animated fadeInUp faster"
      leave-active-class="animated fadeOutDown faster"
    >
      <v-card
        elevation="16"
        color="yellow lighten-5"
        class="mx-auto py-6"
        max-width="300"
        height="290"
        id="create-task"
        v-show="isCreating"
      >
        <v-form class="mx-6 mt-4">
          <v-text-field label="Name" v-model="nameText" />
          <v-text-field label="Task" v-model="taskText" />
          <v-btn
            class="mt-10 mr-2"
            color="light-green darken-1"
            @click="sendForm"
          >
            <p class="title font-weight-bold my-auto white--text">Create</p>
          </v-btn>
          <v-btn class="mt-10 ml-2" color="red darken-1" @click="closeForm">
            <p class="title font-weight-bold my-auto white--text">Cancel</p>
          </v-btn>
        </v-form>
      </v-card>
    </transition>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      nameText: "",
      taskText: "",
      isCreating: false
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
      if (this.nameText.length > 0 && this.taskText.length > 0) {
        const name = this.nameText;
        const task = this.taskText;
        this.$emit("add-todo", {
          name,
          task,
          done: false
        });
        this.newTodoText = "";
      }
      this.isCreating = false;
    }
  }
};
</script>
