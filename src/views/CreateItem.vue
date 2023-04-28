<template>
    <Sidebar />

    <div class="main">
        <div class="container-fluid">
            <div class="row">
                <h5>Create Product</h5>

                <form class="center" @submit.prevent="create">
                    <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Name</label>
                        <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"
                            v-model="name" required>

                    </div>

                    <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Password</label>
                        <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"
                            v-model="description" required>

                    </div>

                    <label class="form-label" for="customFile">Add Image</label>
                    <input type="file" class="form-control" id="customFile" />

                    <div>
                        <button type="submit" class="btn btn-primary">Add Product</button>
                    </div>



                </form>
            </div>

        </div>


    </div>
</template>

<script>
import Sidebar from '../views/Sidenav.vue'
import { Pie } from 'vue-chartjs'

export default {
    // name: 'ParentView',
    components: {
        Sidebar
    },

    data() {
        return {
            name: '',
            description: ''
        }


    },
    methods: {
        async create() {
            const name = this.name;
            const description = this.description;
            const response = await fetch("http://127.0.0.1:8000/api/items", {
                method: "POST",
                headers: {
                    'Authorization': 'Bearer ' + localStorage.getItem('token'),
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({ name , description })
            });

            const data = await response.json();

            // check if post was successful
            if (data.success) {
               
               
                console.log("Success:", data.message);
                this.$router.push({ path: '/products' });
            } else {
                console.error(" failed:", data.message);
            }
        }
    },


    beforeRouteEnter(to, from, next) {
        const token = localStorage.getItem('token');
        if (!token) {
            next('/'); // Redirect to login page
        } else {
            next();
        }
    }
}

</script>

<style scoped>
.main {
    margin-left: 160px;
    /* Same as the width of the sidenav */
    font-size: 28px;
    /* Increased text to enable scrolling */
    padding: 0px 10px;
}

img {
    margin-top: 3%;
    height: 20%;
}

form {
    width: 50%;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    margin-top: 5%;
}
</style>