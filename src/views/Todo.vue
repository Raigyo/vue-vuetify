<template>
  <div class="home">
    <field-add-task />
    <list-tasks v-if="$store.state.tasks.length" />
    <no-task v-else />
  </div>
</template>

<script>
import FieldAddTask from "@/components/ToDo/FieldAddTask";
import ListTasks from "@/components/ToDo/ListTasks";
import NoTask from "@/components/ToDo/NoTask";

export default {
  name: "Home",
  data() {
    return {
      newTaskTitle: "",
    };
  },
  methods: {
    addTask() {
      this.$store.commit("addTask", this.newTaskTitle);
      this.newTaskTitle = "";
    },
  },
  components: {
    "field-add-task": FieldAddTask,
    // "field-add-task": require ("@/components/ToDo/FieldAddTask.vue").default;
    "list-tasks": ListTasks,
    "no-task": NoTask,
  },
};
</script>
