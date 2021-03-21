<template>
<v-container>
    <v-card>
      <div v-show="isEditing">
        <v-card-text>
          <v-text-field type="text"
                        v-model="textTask"
                        clearable
          >
          </v-text-field>
        </v-card-text>
        <v-card-actions>
          <v-checkbox v-model="value"></v-checkbox>
          <v-btn icon @click="closeForm">
            <v-icon>mdi-cancel</v-icon>
          </v-btn>
          <v-btn icon @click="editTask">
            <v-icon>mdi-check</v-icon>
          </v-btn>
        </v-card-actions>
      </div>
      <div v-show="!isEditing">
        <v-card-text v-text="todo.name"></v-card-text>
        <v-spacer></v-spacer>
        <v-card-actions>
          <v-checkbox v-model="value"></v-checkbox>
          <v-btn icon @click="deleteTask(todo)">
            <v-icon>mdi-cancel</v-icon>
          </v-btn>
          <v-btn icon @click="openForm">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
        </v-card-actions>
      </div>
    </v-card>
</v-container>
</template>

<script>
export default {
name: "Todo",
  props: {
    todo: {
      required: true,
      type: Object
    }
  },
  data() {
    return {
      isEditing: false,
      textTask: this.todo.name,
    }
  },

  computed: { //funkcje, które używamy w widoku
    value: {
      get() {
        return this.todo.done;
      },
      set(done) {
        this.$emit('change', {...this.todo, done});
      },
    },
  },
  methods: {
    openForm() {
      this.isEditing = true;
    },
    closeForm() {
      this.isEditing = false;
    },
    deleteTask(todo) {
      this.$emit('delete-task', todo.id );
    },
    editTask(name) {
      name = this.textTask;
      this.$emit('edit-task', {...this.todo, name});//przekazanie propsów i pola
      this.isEditing = false;
    }
  },


};

</script>

<style scoped>

</style>
