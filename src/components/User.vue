<template>
<div class="row" style="padding: 10px; margin-top:50px">
  
  <div class="col-md-4">
    <h2>Adicionar Usuários</h2>
    
    <form @submit="saveUser" class="text-left" style="background-color:#f9f9f9; border: 1px dashed #ddd; padding:20px 15px; margin:10px 0;">
      
      <div class="form-group">
        <label>@Usuário</label>
        <input class="form-control" type="text" v-model="username" >
      </div>
      <div class="form-group">
        <label>Email</label>
        <input class="form-control" type="email" v-model="email" >
      </div>
      <div class="form-group">
        <label>Primeiro Nome</label>
        <input class="form-control" type="text" v-model="first_name" >
      </div>
      <div class="form-group">
        <label>Sobrenome</label>
        <input class="form-control" type="text" v-model="last_name" >
      </div>

      <button type="submit" class="btn btn-sm btn-success">Confirmar</button>

    </form>
  
  </div><!-- col -->
  
  <div class="col-md-7">
      <div class="lead text-left">
        <strong v-if="users.results">Total de usuários: {{ users.results.length }}</strong>
      </div>
      <table class="table table-condensed">
        <thead>
          <tr>
            <th>ID</th>
            <th>Username</th>
            <th>Nome</th>
            <th>Email</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in users.results" v-bind:key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.username }}</td>
            <td>{{ item.first_name }}</td>
            <td>{{ item.email }}</td>
          </tr>
        </tbody>
      </table>
  </div><!-- col -->
</div><!-- row -->
</template>

<script>
// https://github.com/axios/axios
import axios from 'axios'

export default {
  name: 'User',
  data() {
    return {
      users: [],
      username: "",
      email: "",
      first_name: "",
      last_name: "",
    }
  },
  created(){
    axios.get('http://127.0.0.1:3000/api/users/create/').then((response) => {
        this.users = response.data;
        return this.users;
        
    })
  },
  methods: {
    saveUser(e) {
      e.preventDefault();
      
      axios.post('http://127.0.0.1:3000/api/users/create/', 
        {
          username: this.username,
          email: this.email,
          first_name: this.first_name,
          last_name: this.last_name,
        }, 
        {
          headers: { Authorization: 'Token e49df3f06c060e10a8b7154f16a88cefebc35da1' }
        }
      ).then(response => {
        //update list
        this.users.push(response);

      })
    }
  }
}



</script>