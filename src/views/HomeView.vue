<template>
  <h1>Users</h1>
  <div class="table-wrapper">
    <table class="table table-hover">
      <thead>
        <tr>
          <th>id</th>
          <th>name</th>
          <th>e-mail</th>
        </tr>
      </thead>
      <tbody v-if="users">
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.id }}</td>
          <td>
            <!-- <td v-if="typeof post.user !== 'undefined'"> -->
            <router-link :to="{ name: `user`, params: { userId: user.id } }">
              {{ user.name }}
            </router-link>
          </td>
          <!-- <td v-else>Anonymouse</td> -->

          <td>
            {{ user.email }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HomeView",
  data() {
    return {
      users: [],
    };
  },
  mounted() {
    this.loadData();
  },
  methods: {
    async loadData() {
      const uri = "https://jsonplaceholder.typicode.com/users";
      const res = await fetch(uri);
      this.users = await res.json();
    },
  },
};
</script>
<style>
body {
  background: rgb(175, 228, 206);
}
h1 {
  font-size: 32px;
  font-family: Arial, Helvetica, sans-serif;
  color: #090;
  font-weight: lighter;
}

a {
  font-weight: bold;
  color: #2c3e50;
}
a.router-link-exact-active {
  color: #307556;
}

.table-wrapper {
  margin: 10px 50px 50px;
  overflow-y: auto;
  max-height: 70vh;
}

.table {
  border-radius: 5px;
  font-size: 12px;
  font-weight: normal;
  border: none;
  border-collapse: collapse;
  width: 100%;
  max-width: 100%;
  white-space: nowrap;
  background-color: white;
}

.table td,
.table th {
  text-align: center;
  padding: 8px;
}

.table thead th {
  color: black;
  background: #4fc3a1;
  position: sticky;
  top: 0;
  z-index: 1;
}

.table thead th:nth-child(odd) {
  color: white;
  background: rgb(36, 69, 57);
}

.table tr:nth-child(even) {
  background: #f8f8f8;
}
</style>
