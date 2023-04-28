<template>
    <Sidebar />

    <div class="main">
        <div class="container-fluid">
            <div class="row">
                <h5>Update Product {{ $route.params.itemId }}</h5>

                <form class="center" @submit.prevent="update">
                    <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Name</label>
                        <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"
                            v-model="item.name" required>

                    </div>

                    <div class="mb-3">
                        <label for="exampleInputEmail1" class="form-label">Description</label>
                        <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp"
                            v-model="item.Description" required>

                    </div>

                    <label class="form-label" for="customFile">Add Image</label>
                    <input type="file" class="form-control" id="customFile" @change="onFileChange" ref="fileInput" />

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
            item: {

                name: '',
                Description: '',
                file: null,

            }

        }
    },

    mounted() {
        this.fetchItem()
    },



    methods: {
        onFileChange(event) {
            this.file = event.target.files[0];
        },

        async fetchItem() {
            try {
                const response = await fetch(`${BASE_URL}/api/item/` + this.$route.params.itemId, {
                    headers: {
                        'Authorization': 'Bearer ' + localStorage.getItem('token'),
                        'Content-Type': 'application/json'
                    }
                });

                const data = await response.json();
                if (data.success) {
                    this.items = data.item;
                    console.log(this.item = data.item[0]);
                } else {
                    console.error(data.message);
                }
            } catch (error) {
                console.error(error);
            }
        },

        async update() {
            const name = this.item.name;
            const description = this.item.Description;

            const response = await fetch(`${BASE_URL}/api/updateItem/` + this.$route.params.itemId, {
                method: "PUT",
                headers: {
                    'Authorization': 'Bearer ' + localStorage.getItem('token'),
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({ name , description })
            });

            const data = await response.json();

            // check if update was successful
            if (data.success) {


                console.log("Success:", data.message);
                this.$router.push({ path: '/products' });
            } else {
                console.error(" failed:", data.message);
            }
        },
        

        // async update() {
        //     const formData = new FormData();
        //     formData.append('name', this.item.name);
        //     formData.append('description', this.item.Description);
        //     formData.append('image', this.item.file)

        //     const response = await fetch("http://127.0.0.1:8000/api/updateItem/" + this.$route.params.itemId, {
        //         method: "PUT",
        //         headers: {
        //             'Authorization': 'Bearer ' + localStorage.getItem('token'),
        //         },
        //         body: formData
        //     });

        //     const data = await response.json();

        //     // check if post was successful
        //     if (data.success) {
        //         console.log("Success:", data.message);
        //         this.$router.push({ path: '/products' });
        //     } else {
        //         console.error(" failed:", data.message);
        //         console.log(this.item.file)
        //     }
        // }





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

@media only screen and (max-width: 400px) {
    .main {
    margin-left: 1px;
    /* Same as the width of the sidenav */
    font-size: 28px;
    /* Increased text to enable scrolling */
    padding: 0px 10px;
    }
}
</style>