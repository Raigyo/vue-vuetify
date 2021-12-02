<template>
  <v-list flat class="pt-0">
    <v-subheader>List of tasks</v-subheader>
    <v-divider></v-divider>
    <!-- <task v-for="task in $store.state.tasks" :key="task.id" :task="task" /> -->
    <draggable v-model="tasks" handle=".handle">
      <task v-for="task in tasks" :key="task.id" :task="task" />
    </draggable>
  </v-list>
</template>

<script>
import draggable from "vuedraggable";
import Task from "@/components/ToDo/Task";
export default {
  computed: {
    tasks: {
      get() {
        return this.$store.getters.tasksFiltered;
      },
      set(value) {
        this.$store.dispatch("setTasks", value);
      },
    },
  },
  components: {
    task: Task,
    draggable,
  },
};
</script>
