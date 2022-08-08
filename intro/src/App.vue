<template>
  <div id="app">
  <HelloWorld msg="User List"/>
  <userList />
  <userAdd />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import userList from './components/userList.vue'
import userAdd from './components/userAdd.vue'



export default {
  name: 'App', 
  components: {
    HelloWorld,
    userList,
    userAdd,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
