<template>
  <v-dialog :value="true" persistent max-width="290">
    <v-card>
      <v-card-title class="text-h5">Edit task</v-card-title>
      <v-card-text
        >Edit the title of this task:
        <v-text-field v-model="taskTitle" @keyup.enter="saveEditedTask" />
      </v-card-text>

      <v-card-actions class="justify-center">
        <v-spacer></v-spacer>
        <v-btn @click="$emit('close')" text> Cancel! </v-btn>
        <v-btn
          @click="saveEditedTask"
          :disabled="taskTitleInvalid"
          color="red darken-1"
          text
        >
          Save task!
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: ["task"],
  data() {
    return {
      taskTitle: null,
    };
  },
  // Computed props let us compose reactive new data from other data
  computed: {
    taskTitleInvalid() {
      return !this.taskTitle || this.taskTitle === this.task.title;
    },
  },
  methods: {
    saveEditedTask() {
      if (!this.taskTitleInvalid) {
        let payload = {
          id: this.task.id,
          title: this.taskTitle,
        };
        this.$store.dispatch("updateTaskTitle", payload);
        this.$emit("close");
        this.$vuetify.goTo(0, { duration: 0 });
      }
    },
  },
  mounted() {
    this.taskTitle = this.task.title;
  },
};
</script>

<style></style>
