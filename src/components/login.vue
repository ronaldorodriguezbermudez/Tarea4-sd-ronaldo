<template>
    <form @submit.prevent="submitForm">
      <h2>Login</h2>
      <div class="input-field">
        <input type="text" v-model="username" placeholder="Enter Username">
      </div>
      <div class="input-field">
        <input type="password" v-model="password" placeholder="Enter Password">
      </div>
      <input type="submit" value="LogIn">
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        username: '',
        password: ''
      }
    },
    methods: {
      submitForm() {
        // Handle form submission here
        // You might want to call an authentication service here
        console.log(`Username: ${this.username}, Password: ${this.password}`);
      }
    }
  }
  </script>
  
  <style scoped>
  /* Add your CSS styles here */
  </style>

