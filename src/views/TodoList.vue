<template>
  <v-container>
    <v-row>
      <p class="title" v-text="title" size></p>
    </v-row>
    <v-row>
      <create-task v-on:create-task="createTask">

      </create-task>
    </v-row>
    <v-row>
      <todo v-for="todo in todos"
            :key="todo.id"
            :todo="todo"
            @change="update($event)"
            v-on:delete-task="deleteTask($event)"
            v-on:edit-task="editTask($event)"
      ></todo>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

import Todo from "@/components/Todo";
import CreateTask from "@/components/CreateTask";
export default {
name: "TodoList",
  components: {
    CreateTask,
    Todo
  },
  props: {
    id: {
      required: true,
      type: [String, Number]
    },
    title:{
      required: true,
      type: String
    }
  },
  data() {
    return {
      todos: [],
      name: this.title,
    };
  },
  async created() {
    try{
      const response = await axios.get(`http://127.0.0.1:8000/api/v1/todos/todos/?todo_list=${this.id}`);
      this.todos = response.data;

    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async update(todo) {
      try{
        const response = await axios.patch(`http://127.0.0.1:8000/api/v1/todos/todos/${todo.id}/` ,todo);
        this.todos = this.todos.map(
            item => item.id === todo.id ? response.data : item
        );
      } catch (err) {
        console.log(err)
      }
      console.log(todo);
    },
    async deleteTask(todo) {
      try {
        await axios.delete(`http://127.0.0.1:8000/api/v1/todos/todos/` + todo)
        this.all();
      } catch (err) {
        console.log(err);
      }
    },
    async createTask(newTodo) {
      try {
        await axios.post(`http://127.0.0.1:8000/api/v1/todos/todos/`, {
          "name": newTodo.task,
          "done": false,
          "todo_list": this.id
        });
        this.all();
      } catch (err) { console.log(err); }
    },
    async editTask(newTodo) {
      try {
        await axios.patch(`http://127.0.0.1:8000/api/v1/todos/todos/${newTodo.id}/`, newTodo);
        this.all();
      } catch (err) { console.log(err); }
    },
    all: function () { //funkcja do odświerzania widoku
      try {
          axios.get(`http://127.0.0.1:8000/api/v1/todos/todos/?todo_list=${this.id}`).then(response => {
          this.todos = response.data;
        })
      } catch (err) { console.log(err); }
    }

}
};
</script>

<style scoped>

</style>
