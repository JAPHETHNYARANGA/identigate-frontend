<template>
    <div class="sidenav">
        <!-- <router-link to="/dashboard">
            DashBoard
        </router-link> -->
        <a href="#" @click.prevent="navigateToProducts">Products</a>
        <a href="#" @click.prevent="logout">Logout</a>



    </div>
</template>

<style scoped>
.sidenav {
    height: 100%;
    width: 160px;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    background-color: #111;
    overflow-x: hidden;
    padding-top: 20px;
}

.sidenav a {
    padding: 6px 8px 6px 16px;
    text-decoration: none;
    font-size: 25px;
    color: #818181;
    display: block;
}

.sidenav a:hover {
    color: #f1f1f1;
}

@media only screen and (max-width: 400px) {
 .sidenav{
    display: none;
 }
}
</style>

<script>
import { BASE_URL } from '../constants';

export default {
    name: 'SidebarView',

    methods: {
        async navigateToProducts() {
            this.$router.push('/products');
        },

        

        async logout() {


            // Make request to logout endpoint
            const response = await fetch(`${BASE_URL}/api/logout`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    Authorization: `Bearer ${localStorage.getItem('token')}`,
                },
            });



            const data = await response.json();

            if (data.success) {
                console.log('Logged out successfully:', data.message);
                // Remove token from local storage
                localStorage.removeItem('token');

                // Redirect to login page
                this.$router.push('/');
            } else {
                console.error('Logout failed:', data.message);
            }
        }
    }
}
</script>