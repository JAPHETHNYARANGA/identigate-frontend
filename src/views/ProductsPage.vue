<template>
    <Sidebar />

    <div class="main">
        <div class="container-fluid">



            <div class="row">
                <p>Products Page</p>

                <div class="col-md-2">
                    <div class="btn btn-success" @click.prevent="addItem">
                        Add Item
                    </div>
                    <button class="btn btn-success  m-3" @click="fetchItems">Search</button>
                </div>
                <div class="col-md-10">
                   

                        <div class="form-outline m-3 mb-4">
                            <input type="search" class="form-control" id="datatable-search-input" placeholder="search here"
                                v-model="searchText">
                        </div>

                        

                    



                </div>

                <div class="row">
                    <div class="col-md-3 " v-for="item in items" :key="item.id">
                        <div class="card shadow-lg p-3 mb-5 bg-white rounded">
                            <div class="d-flex justify-content-center">
                                <img class="card-img-top" :src="getImageUrl(item.image)" alt="item image">
                            </div>
                            <div class="card-body">
                                <h5 class="card-title">{{ item.name }}</h5>
                                <p class="card-text">{{ item.Description }}</p>
                                <div class="row">
                                    <div class="col-6">
                                        <a @click.prevent="updateItem(item.id)" class="btn btn-success">Update</a>
                                    </div>
                                    <div class="col-6">
                                        <a @click.prevent="deleteItem(item.id)" class="btn btn-danger">Delete</a>
                                    </div>
                                </div>

                            </div>
                        </div>

                    </div>




                </div>

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
            items: [],
            searchText: ''
        };
    },
    mounted() {
        this.fetchItems()
    },

    computed: {
        filteredItems() {
            return this.items.filter(item => {
                return item.name.toLowerCase().includes(this.searchText.toLowerCase())
            })
        }
    },
    methods: {

        getImageUrl(imageName) {
            if (!imageName) {
                return '';
            }
            return `${BASE_URL}/storage/${imageName.replace("public/", "")}`;
        },


        async fetchItems() {
            try {

                const url = `${BASE_URL}/api/items?search=${this.searchText}`
                const response = await fetch(url, {
                    headers: {
                        'Authorization': 'Bearer ' + localStorage.getItem('token'),
                        'Content-Type': 'application/json'
                    }
                });

                const data = await response.json();
                if (data.success) {
                    this.items = data.items;
                } else {
                    console.error(data.message);
                }
            } catch (error) {
                console.error(error);
            }
        },

        async deleteItem(itemId) {
            console.log('delete', itemId)

            try {
                const response = await fetch(`${BASE_URL}/api/deleteItem/${itemId}`, {
                    headers: {
                        'Authorization': 'Bearer ' + localStorage.getItem('token'),
                        'Content-Type': 'application/json'
                    }
                });
                const data = await response.json();
                if (data.success) {
                    this.fetchItems()
                } else {
                    console.error(data.message);
                }

            } catch (error) {
                console.error(error);
            }

        },

        async addItem() {
            this.$router.push('/create');
        },
        async updateItem(itemId) {
            this.$router.push({
                name: 'update',
                params: { itemId: itemId }
            });

        },

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
    height: 5rem;
    width: 5rem;
    text-align: center;
}

.search-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    width: 100%;
}
</style>