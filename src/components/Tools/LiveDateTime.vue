<template>
  <v-row class="text-subtitle-1 ml-2">{{ date }}</v-row>
</template>

<script>
import { format } from "date-fns";
export default {
  data() {
    return {
      date: "",
    };
  },
  methods: {
    getDate() {
      this.date = format(new Date(), "d MMMM Y, H:mm:ss");
      setTimeout(this.getDate, 1000);
    },
  },
  mounted() {
    this.getDate();
  },
};
</script>

<style></style>
