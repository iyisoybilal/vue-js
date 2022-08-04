<template>
    <div>
        <form @submit.prevent="formSubmit" class="control-form">
            <h2>Update user</h2>
        <input type="text" v-model="updateUser.firstname" /> <br />
        <input type="text" v-model="updateUser.lastname" /> <br />
        <input type="text" v-model="updateUser.email" /> <br />
        <input type="text" v-model="updateUser.password" /> <br />

  <button @click="updateUser">Update</button>
        </form>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
          data(){
            return {
                updateUser:{
                    firstName:"",lastName:"",email:"",password:"" 
                }
            }
        },
        methods:{
           async formSubmit() {
             try {
            const user = await axios.put(
             "http://localhost:8080/user/" + this.user._id,
             {
                name: this.updateUser.firstname,
                lastname:this.updateUser.lastName,
                email: this.updateuser.email,
                password:this.updateUser.password
            }
        );

            console.log(user.data);
            alert("User updated!");
         } catch (e) {
          console.log(e);
  }
},

        }
  
    }
</script>

<style scoped>

</style>