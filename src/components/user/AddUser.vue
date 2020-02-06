<template>
<div>
    <h2>Adicionar Usuários</h2>
    
    <form @submit.prevent="saveUser" @on:keyup.enter="submit" class="text-left" style="background-color:#f9f9f9; border: 1px dashed #ddd; padding:20px 15px; margin:10px 0;">
    
    <div class="form-group">
        <label>@Usuário</label>
        <input class="form-control" type="text" v-model="user.username" >
    </div>
    <div class="form-group">
        <label>Email</label>
        <input class="form-control" type="email" v-model="user.email" >
    </div>
    <div class="form-group">
        <label>Primeiro Nome</label>
        <input class="form-control" type="text" v-model="user.first_name" >
    </div>
    <div class="form-group">
        <label>Sobrenome</label>
        <input class="form-control" type="text" v-model="user.last_name" >
    </div>

    <button type="submit" class="btn btn-sm btn-success">Confirmar</button>

    </form>

</div>
</template>
  


<script>

import { eventBus } from '../../main';

// https://github.com/axios/axios
import axios from 'axios'


export default {
  name: 'AddUser',
  data() {
    return {
      user: {
        username: "",
        email: "",
        first_name: "",
        last_name: "",
      },
    }
  },
  methods: {
    saveUser() {
      
      var data = {
          username: this.user.username,
          email: this.user.email,
          first_name: this.user.first_name,
          last_name: this.user.last_name,
      };
      
      axios.post('http://127.0.0.1:3000/api/users/create/', data, 
        {
          headers: { Authorization: 'Token e49df3f06c060e10a8b7154f16a88cefebc35da1' }
        }
      ).then((response) => {
        // enviando dados para outros components
        eventBus.$emit('submit', response.data);
        
      })
    },
  }
}


</script>