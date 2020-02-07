<template>
  <div>
    <div class="row justify-content-md-center">
      <div class="col-md-4">
        <!-- <AddUser /> -->
        <form @submit.prevent="saveUser" @on:keyup.enter="submit" class="text-left my-form">
          <div class="form-group">
            <label>@Usuário</label>
            <input class="form-control" type="email" v-model="user.username">
          </div>
          <div class="form-group">
            <label>Email</label>
            <input class="form-control" type="email" v-model="user.email">
          </div>
          <div class="form-group">
            <label>Primeiro Nome</label>
            <input class="form-control" type="text" v-model="user.first_name">
          </div>
          <div class="form-group">
            <label>Sobrenome</label>
            <input class="form-control" type="text" v-model="user.last_name">
          </div>
          <button type="submit" class="btn btn-sm btn-success">Confirmar</button>
        </form>
      </div>
      <div class="col-md-7">
        <div class="lead text-left">
          <strong v-if="users.results">Total de usuários: {{ users.results.length }}</strong>
        </div>
        <div>
          <table class="table table-condensed">
            <thead>
              <tr>
                <th>ID</th>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Email</th>
                <th>Username</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in users.results" v-bind:key="item.id">
                <td>{{ item.id }}</td>
                <td>{{ item.first_name }}</td>
                <td>{{ item.last_name }}</td>
                <td>{{ item.email }}</td>
                <td>{{ item.username }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div><!-- row -->
</template>
<script>
// import { eventBus } from '../../main';
import axios from 'axios'

export default {
  name: 'UserList',
  data() {
    return {
      users: [],
      user: {
        username: "",
        email: "",
        first_name: "",
        last_name: "",
      }
    }
  },
  created() {
    axios.get('http://127.0.0.1:8000/api/users/create/').then((response) => {
      this.users = response.data;
    })
    // var vm = this;
    // recebendo dados de outros componentes
    // eventBus.$on('submit', function (response) {
    //   console.log(response);
    //   // dando erro de push is not a function
    //   vm.users.push(response);
    // })

  },
  methods: {
    saveUser() {
      var data = {
          username: this.user.username,
          email: this.user.email,
          first_name: this.user.first_name,
          last_name: this.user.last_name,
      };
      axios.post('http://127.0.0.1:8000/api/users/create/', data, 
        {
          headers: { Authorization: 'Token 57682aa526aa16907a582bb5773db67adf95920e' }
        }
      ).then(response => {
        this.users.results.push(response.data);
      })
    }
  }
}
</script>
<style>
.my-form {
  background-color: #f9f9f9;
  border: 1px dashed #ddd;
  padding: 20px 15px;
  margin: 10px 0;
}
</style>