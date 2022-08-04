<template>
    
    <div id="app">
        <table border="1px" class="table">
          <tr>
          <td>FirstName</td>
          <td>LastName</td>
          <td>Email</td>
          <td>Password</td>
          </tr>
          <tr v-for="user of users" :key="user._id">
          <td>{{user.firstName}}</td>
          <td>{{user.lastName}}</td>
          <td>{{user.email}}</td>
          <td>{{user.password}}</td>
          </tr>
        </table>  
       
    </div>
</template>

<script>
export default {
    created() {
      this.getUsers();
    },
    data() {
      return {
        users: []
      };
    },
    methods: {
      async getUsers() {
        var response = await fetch('http://localhost:8080/user/list')
        var data = await response.json()
        this.users=data
      }
    }
  };
</script>

<style scoped>
.table{
  width: 100%;
}
</style>