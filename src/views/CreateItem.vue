<template>
    <Sidebar />

    <div class="main">
        <div class="container-fluid">
            <div class="row">
                <h5>Create Product</h5>

                <form class="center" @submit.prevent="create" enctype="multipart/form-data">
                    <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Name</label>
                        <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"
                            v-model="name" required>

                    </div>

                    <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Description</label>
                        <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"
                            v-model="description" required>

                    </div>

                    <label class="form-label" for="customFile">Add Image</label>
                    <input type="file" class="form-control" id="customFile" @change="onFileChange" ref="fileInput"
                        />


                   
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
import { BASE_URL } from '../constants';


export default {
    // name: 'ParentView',
    components: {
        Sidebar
    },

    data() {
        return {
            name: '',
            description: '',
            file: null,
        }


    },
    methods: {

        onFileChange(event) {
            this.file = event.target.files[0];
        },
        async create() {
            const formData = new FormData();
            formData.append('name', this.name);
            formData.append('description', this.description); 
            formData.append('image', this.file)

            const response = await fetch(`${BASE_URL}/api/items`, {
                method: "POST",
                headers: {
                    'Authorization': 'Bearer ' + localStorage.getItem('token'),
                    
                },
                body: formData
            });

            const data = await response.json();

            // check if post was successful
            if (data.success) {


                console.log("Success:", data.message);
                this.$router.push({ path: '/products' });
            } else {
                console.error(" failed:", data.message);
                console.log(this.file)
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