<template>
    <div>
      <div class="container-fluid">
  
        <h1>Login </h1>
        <form class="center" @submit.prevent="login">
          <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Email address</label>
            <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"
              v-model="email" required>
  
          </div>
  
          <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Password</label>
            <input type="password" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"
              v-model="password" required>
  
          </div>
  
          <div>
            <button type="submit" class="btn btn-primary">Login</button>
          </div>
  
  
          <router-link to="/register">
            <h6>Don't have an account? Register here</h6>
          </router-link>
        </form>
  
  
      </div>
  
    </div>
  </template>
  
  <style scoped>
  h1 {
    margin-top: 5%;
  }
  
  form {
    width: 60%;
    left: 50%;
    position: absolute;
    transform: translateX(-50%);
  }
  
  .center {
  
    justify-content: center;
    margin-top: 5%;
  }
  
  h6 {
    color: blueviolet;
    margin-top: 3%;
    font-weight: 600;
    font-size: 17px;
    cursor: pointer;
  }
  </style>
  
  <script>
  export default {
    data() {
      return {
        email: '',
        password: '',
      };
    },
    methods: {
      // define a method to handle the login form submission
      async login() {
        const email = this.email;
        const password = this.password;
        const response = await fetch("http://127.0.0.1:8000/api/login", {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify({ email, password })
        });
  
        const data = await response.json();
  
        // check if login was successful
        if (data.success) {
          // store the token in the application
          localStorage.setItem("token", data.token);
          console.log("Success:", data.message);
          this.$router.push({ path: '/dashboard' });
        } else {
          console.error("Login failed:", data.message);
        }
      }
  
    }
  }
  </script>
  