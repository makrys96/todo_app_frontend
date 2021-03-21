<template>
 <v-container><!--  pilnuje odstępów, marginesów-->
    <todo-lists></todo-lists>
  </v-container>
</template>

<script>
// @ is an alias to /src


import TodoLists from "@/components/todo-lists";
export default {
  name: 'Home',
  components: {
    TodoLists

  }
}
</script>
