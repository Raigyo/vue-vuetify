<template>
  <v-list flat class="pt-0">
    <v-subheader>List of tasks</v-subheader>
    <v-divider></v-divider>
    <!-- <task v-for="task in $store.state.tasks" :key="task.id" :task="task" /> -->
    <task
      v-for="task in $store.getters.tasksFiltered"
      :key="task.id"
      :task="task"
    />
  </v-list>
</template>

<script>
import Task from "@/components/ToDo/Task";
export default {
  components: {
    task: Task,
  },
};
</script>
