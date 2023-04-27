<template>
    <div>
      <h1>Login Page</h1>
      <form>
        <div>
          <label>Email:</label>
          <input type="email" v-model="email" required />
        </div>
        <div>
          <label>Password:</label>
          <input type="password" v-model="password" required />
        </div>
        <div>
          <button type="submit" class="btn btn-primary">Login</button>
        </div>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        email: '',
        password: '',
      };
    },
    methods: {
      loginpage() {
        // Implement login functionality here
        console.log('login pressed')
      },
    },
  };
  </script>
  