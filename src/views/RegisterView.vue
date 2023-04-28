<template>
    <div>
        <div class="container-fluid">

            <h1>Register </h1>
            <form class="center" @submit.prevent="register">

                <div class="mb-3">
                    <label for="exampleInputEmail1" class="form-label">Name</label>
                    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"
                        v-model="name" required>

                </div>

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
                    <button type="submit" class="btn btn-primary">Register</button>
                </div>


                <router-link to="/">
                    <h6>Already have an account? Login here</h6>
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
    text-decoration: none;

}
</style>
  
<script>

import { BASE_URL } from '../constants';

export default {
    data() {
        return {
            email: '',
            password: '',
            name: '',
        };
    },
    methods: {
        async register() {
            const email = this.email;
            const password = this.password;
            const name = this.name;
            const response = await fetch(`${BASE_URL}/api/register`, {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({ name, email, password })
            });

            const data = await response.json();

            // check if login was successful
            if (data.success) {
                // store the token in the application
                
                console.log("Success:", data.message);
                this.$router.push({ path: '/' });
            } else {
                console.error("Login failed:", data.message);
            }
        },
    },
};
</script>


  