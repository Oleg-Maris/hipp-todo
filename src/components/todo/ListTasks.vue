<template>
  <v-list class="pt-0" flat>
    <draggable v-model="tasks" handle=".handle">
      <the-task v-for="task in tasks" :key="task.id" :task="task" />
    </draggable>
  </v-list>
</template>

<script>
import draggable from "vuedraggable";

export default {
  components: {
    "the-task": require("@/components/todo/TheTask.vue").default,
    draggable,
  },
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
};
// $store.getters.tasksFiltered
</script>
