<template>
  <div>
    <v-container>
      <h2 class="my-5">Todos</h2>

      <v-row>
        <v-col col="5">
          <v-text-field
            type="date"
            label="Due Date*"
            v-model="newTodoForm.dueDate"
            required/>
        </v-col>
        <v-col col="5">
          <v-text-field
            label="Description*"
            v-model="newTodoForm.description"
            required/>
        </v-col>
        <v-col col="2">
          <v-btn @click="createTodo">Create</v-btn>
        </v-col>
      </v-row>

      <v-data-table
        :headers="headers"
        :items="todos"
        :items-per-page="5"
        class="elevation-1"
      >
        <template v-slot:item.actions="{item}">
          <v-icon small @click="deleteTodo(item)"> mdi-delete </v-icon>
        </template>
      </v-data-table>
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
      { text: "", value: "actions", sortable:false}
    ],
    newTodoForm: {
      dueDate: '',
      description: '',
      completed: false
    }
  }),
  methods: {
    async getTodos() {
      const { data } = await axios.get(
        "https://jk-express-todo-api.herokuapp.com/api/v1/todos"
      );
      this.todos = data;
    },
    async createTodo() {
      await axios.post('https://jk-express-todo-api.herokuapp.com/api/v1/todos/create', this.newTodoForm);
      
      this.newTodoForm.dueDate = '';
      this.newTodoForm.description = '';
      await this.getTodos();
    },
    async deleteTodo(todo) {
      await axios.delete('https://jk-express-todo-api.herokuapp.com/api/v1/todos/delete/'+todo._id);
      await this.getTodos();
    }
  },
};
</script>