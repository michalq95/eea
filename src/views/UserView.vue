<template>
  <router-link to="/">Return</router-link>

  <h1>{{ this.user.name }}</h1>
  <button @click="this.i++">Filter by status</button>
  <div class="table-wrapper">
    <table class="table table-hover">
      <thead>
        <tr>
          <th>id</th>
          <th>title</th>
          <th @click="this.i++">completed</th>
        </tr>
      </thead>
      <tbody v-if="todos">
        <tr v-for="todo in displayedTodos" :key="todo.id">
          <td>{{ todo.id }}</td>
          <td>{{ todo.title }}</td>

          <td>
            {{ todo.completed }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      user: Object,
      todos: [],
      i: 0,
    };
  },
  mounted() {
    this.loadData();
  },
  props: {
    userId: String,
  },
  methods: {
    async loadData() {
      let uri = `https://jsonplaceholder.typicode.com/users/${this.userId}`;
      let res = await fetch(uri);
      this.user = await res.json();
      uri = `https://jsonplaceholder.typicode.com/users/${this.userId}/todos`;
      res = await fetch(uri);
      this.todos = await res.json();
    },
  },
  computed: {
    displayedTodos() {
      if (this.i % 3 == 0) return this.todos;
      if (this.i % 3 == 1) return this.todos.filter((t) => !t.completed);
      if (this.i % 3 == 2) return this.todos.filter((t) => t.completed);
    },
  },
};
</script>
<style>
nav a {
  font-weight: bold;
  color: #2c3e50;
}
</style>
