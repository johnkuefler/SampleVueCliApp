<template>
  <div>
    <v-container>
      <h2 class="my-5">Todos</h2>
      <v-data-table
        :headers="headers"
        :items="todos"
        :items-per-page="5"
        class="elevation-1"
      ></v-data-table>
    </v-container>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "TodosTable",
  mounted() {
    this.getTodos();
  },
  data: () => ({
    todos: [],
    headers: [
      { text: "Due Date", value: "dueDate" },
      { text: "Description", value: "description" },
      { text: "Complete", value: "completed" },
    ],
  }),
  methods: {
    async getTodos() {
      const { data } = await axios.get(
        "https://jk-express-todo-api.herokuapp.com/api/v1/todos"
      );
      this.todos = data;
    },
  },
};
</script>