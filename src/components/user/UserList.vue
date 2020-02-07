<template>
  <div>
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
</template>
  


<script>

import { eventBus } from '../../main';

// https://github.com/axios/axios
import axios from 'axios'

export default {
  name: 'UserList',
  data() {
    return {
      users: [],
    }
  },
  created() {
    this.getUsers();

    var vm = this;
    // recebendo dados de outros componentes
    eventBus.$on('submit', function(response) {
      console.log(response);
      vm.users.push(response);
    })
  },
  methods: {
    getUsers: async function() {
      axios.get('http://127.0.0.1:3000/api/users/create/').then((response) => {
        this.users = response.data;
          
      })
    },
  }
}

</script>