<template>
  <v-container>
    <v-row>
      <v-col v-for="todoList in todoLists"
             :key="todoList.id"
              cols="12" xs="12" md="3">
        <todo-list :todoList="todoList"
                   v-on:delete-todo="deleteTodo"
                   v-on:edit-todo="editTodo"

        >
        </todo-list>
      </v-col>
      <v-col cols="12" xs="12" md="3">
        <create-todo v-on:create-todo="createTodo">

        </create-todo>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

import TodoList from '@/components/todo-list';
import CreateTodo from "@/components/CreateTodo";

export default {
  components: {
    TodoList,
    CreateTodo
  },
  data() {
    return {
      todoLists: [] //  tworzenie nowej listy
    };
  },
  async created() {
    try{
      const response = await axios.get('http://127.0.0.1:8000/api/v1/todos/todo-lists/');
      this.todoLists = response.data;
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async deleteTodo(todoList) {
      try {
        await axios.delete(`http://127.0.0.1:8000/api/v1/todos/todo-lists/` + todoList);
        this.all();
      }catch (err) {
        console.log(err)
      }
    },
    async createTodo(newTodo) {
      await axios.post(`http://127.0.0.1:8000/api/v1/todos/todo-lists/`, {
        "name": newTodo.title,
        "description": newTodo.project
      });
      this.all();
    },
    async editTodo(newTodo){
      await axios.patch(`http://127.0.0.1:8000/api/v1/todos/todo-lists/${newTodo.id}/`, newTodo)
    },
    all: function () { //funkcja do odświerzania widoku
      try {
        axios.get(`http://127.0.0.1:8000/api/v1/todos/todo-lists/`).then(response => {
          this.todoLists = response.data;
        })
      } catch (err) { console.log(err); }
    }
  }
};
</script>


<style scoped>

</style>
