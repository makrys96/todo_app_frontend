<template>
<v-container>
  <v-card>
    <v-text-field type="text"
                  v-model="taskText"
                  clearable

    >
    </v-text-field>
    <v-btn icon
           @click="sendForm()">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
  </v-card>
</v-container>
</template>

<script>
export default {
  data() {
    return {
      taskText: '',
      done: false,
    }
  },
  methods: {
    sendForm() {
      const task = this.taskText;
      this.$emit('create-task', {
        task,
        done: false,
      })
    }
  }
}
</script>

<style scoped>

</style>
