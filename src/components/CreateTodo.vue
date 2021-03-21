<template>
  <v-card >
    <v-icon @click="openForm" v-show="!isCreating">mdi-plus</v-icon>
    <div v-show="isCreating">
    <v-card-text>
      <v-text-field type="text"
                    v-model="titleText"
      ></v-text-field>
      <v-text-field type="text"
                    v-model="projectText"
      ></v-text-field>
    </v-card-text>
    <v-card-actions>
      <v-btn icon
             @click="sendForm()">
        <v-icon>mdi-plus</v-icon>
      </v-btn>
      <v-btn icon
             @click="closeForm">
        <v-icon>mdi-cancel</v-icon>
      </v-btn>
    </v-card-actions>
    </div>
  </v-card>

</template>

<script>
export default {
  data() {
    return {
      titleText: '',
      projectText: '',
      isCreating: false,
    }
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
      if (this.titleText.length > 0 && this.projectText.length > 0) {
        const title = this.titleText;
        const project = this.projectText;
        this.$emit('create-todo', {
          title,
          project
        });
        this.titleText = '';
        this.projectText = '';
        this.isCreating = false;
      } else {
        this.isCreating = false;
      }
    }
  }
}
</script>

<style scoped>

</style>
