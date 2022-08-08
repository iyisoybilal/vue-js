<template>
    
    <div id="app">
        <table border="1px" class="table">
          <tr class="tr">
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
            <button id="button" class="btn btn-sm btn-danger" @click="Sil(user._id)">Sil</button>
            <button id="button" class="btn btn-warning btn-sm" @click="()=>{
              this.updateUser = user}">Güncelle</button>
          </tr>
        </table>  
          <form @submit.prevent="" class="control-form">
              <h2>Update user</h2>
              <input type="text" v-model="updateUser.firstName" /> <br />
              <input type="text" v-model="updateUser.lastName" /> <br />
              <input type="text" v-model="updateUser.email" /> <br />
              <input type="password" v-model="updateUser.password" /> <br />
              <button @click="userUpdate()" class="btn btn-success">Update</button>
        </form>
    </div>
</template>

<script>
export default {
    created() {
      this.getUsers();
    },
    data() {
      return {
        users: [],
        updateUser: []
      };
    },
    methods: {
      async getUsers() {
        var response = await fetch('http://localhost:8080/user/list')
        var data = await response.json()
        this.users=data
        await this.getUsers();
      },
        async Sil(id){
        await fetch('http://localhost:8080/user/del/'+ id, {
        method:'DELETE'});
        await this.getUsers();
      },
      async userUpdate(){
        if(this.updateUser.length == 0){
          alert("Lütfen Kullanıcı Seçiniz");
          return;
        }
        var myHeaders = new Headers();
        myHeaders.append("Content-Type", "application/json");

        var raw = JSON.stringify(this.updateUser);

        var requestOptions = {
          method: 'POST',
          headers: myHeaders,
          body: raw,
          redirect: 'follow'
        };

        await fetch("http://localhost:8080/user/update/"+this.updateUser._id, requestOptions)
          .then(response => response.text())
          .then(result => console.log(result))
          .catch(error => console.log('error', error));
        await this.getUsers();
      }
    }
  };
</script>

<style scoped>
.table{
  width: 100%;
}
#button{
  width: 100%;
  height: 100%;
  background-color: rgb(113, 110, 110);
  color: white;
}
.control-form{
  margin-left: 850px;
}
.tr{
  color:red;
}
#btn btn-sm btn-danger{
  background-color: red;
}
</style>