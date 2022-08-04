<template>
    <div>
        <form @submit.prevent="submitForm" class="form-control">
        <label for="fname">FirstName:</label>
        <input name="firstName" type="text" v-model="newUser.firstName" /> <br>
        <label for="lname">LastName:</label> 
        <input name="lastName" type="text" v-model="newUser.lastName" /> <br>
        <label for="email" class="email">Email:</label>
        <input name="email" type="text" v-model="newUser.email"  /> <br>
        <label for="password" class="password">Password:</label>
        <input name="password" type="text" v-model="newUser.password" /> <br>
        <button type="submit">Ekle</button>
        </form>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                newUser:{
                    firstName:"",lastName:"",email:"",password:"" 
                }
            }
        },
        methods:{
           async submitForm(){
            console.log("çalıştı")
            var response = await fetch('http://localhost:8080/user/register', {
             method: 'POST',
             headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
            },
            body: JSON.stringify(this.newUser)
        })
            console.log(await response.json())
            }

        }
    }
</script>

<style scoped>
.form-control{
    display: inline-block;
    margin-right: 1200px;
}
.email{
    padding-right: 33px;
    
}
.password{
    padding-right: 3px;
}
</style>