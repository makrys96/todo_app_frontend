<template>
  <v-card>
    <div v-show="isEditing">
      <v-card-title>
        <v-text-field type="text" v-model="newTodo.name"></v-text-field>
        <v-text-field type="text" v-model="newTodo.description"></v-text-field>
      </v-card-title>
      <v-card-actions>
        <v-btn icon @click="closeForm">
          <v-icon>mdi-close</v-icon>
        </v-btn>
        <v-btn icon @click="editTodo">
          <v-icon>mdi-check</v-icon>
        </v-btn>
      </v-card-actions>
    </div>
    <div v-show="!isEditing">
      <v-card-title v-text="todoList.name"></v-card-title>
      <v-card-text>
        <p v-text="todoList.description"></p>
        <p>
          <span v-text="todoList.number_of_done_tasks"></span>/
          <span v-text="todoList.number_of_tasks"></span>
        </p>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn icon @click="openForm">
          <v-icon>mdi-pencil</v-icon>
        </v-btn>
        <v-btn icon @click="deleteTodo(todoList)">
          <v-icon>mdi-cancel</v-icon>
        </v-btn>
        <v-btn icon
               :to="{ name: 'TodoList', params: { id: todoList.id, title: todoList.name}}"
        >
          <v-icon>mdi-arrow-right</v-icon>
        </v-btn>

      </v-card-actions>
    </div>
  </v-card>

</template>

<script>
export default {
  props: {
    todoList: {
      required: true,
      type: Object
    }

  },
  data() {
    return {
      isEditing: false,
      newTodo: this.todoList,
    }
  },
  methods: {
    openForm(){
      this.isEditing = true;
    },
    closeForm() {
      this.isEditing = false;
    },
    deleteTodo(todoList) {
      this.$emit('delete-todo', todoList.id );
    },
    editTodo(todo) {
      todo = this.newTodo;
      this.$emit('edit-todo', {...this.todoList, todo});
      this.isEditing = false;
    }
  },
};
</script>

<style scoped>

</style>
