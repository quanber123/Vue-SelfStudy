<template>
  <div class="container">
    <div class="row">
      <div class="card col">
        <div class="card-header bg-light text-white">
          <form @submit.prevent="handleRegister">
            <input class="form-control" type="text" v-model="user.name" />
            <input class="form-control" type="email" v-model="user.email" />
            <input
              class="form-control"
              type="password"
              v-model="user.password"
            />
            <button class="form-control bg-success text-white" type="submit">
              Register
            </button>
          </form>
        </div>
      </div>
      <div v-for="user in users" :key="user.id">
        <h1>{{ user.name }}</h1>
        <button class="btn btn-danger" @click="filteredUsers(user.id)">
          Delete User
        </button>
        <button v-if="!user.editing" @click="editUser(user)">Edit User</button>
        <div v-if="user.editing">
          <input class="form-control" type="text" v-model="user.name" />
          <input class="form-control" type="email" v-model="user.email" />
          <input class="form-control" type="password" v-model="user.password" />
          <button class="btn btn-success" @click="saveUser(user)">Save</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Register',
  data() {
    return {
      user: {
        name: '',
        email: '',
        password: '',
      },
      users: [],
    };
  },
  methods: {
    handleRegister() {
      const newUser = {
        ...this.user,
        id: new Date().getTime(),
        editing: false,
      };
      this.users = [...this.users, newUser];
      console.log(this.users);
      this.user = { name: '', email: '', password: '' };
    },
    filteredUsers(id) {
      this.users = this.users.filter((user) => user.id !== id);
    },
    editUser(user) {
      user.editing = true;
    },
    saveUser(user) {
      user.name = user.name;
      user.email = user.email;
      user.password = user.password;
      user.editing = false;
    },
  },
};
</script>
