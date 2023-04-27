<template>
    <div>
        <div class="container-fluid">

            <h1>Register </h1>
            <form class="center">

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
export default {
    data() {
        return {
            email: '',
            password: '',
            name:'',
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


  