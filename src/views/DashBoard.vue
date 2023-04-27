<template>
    <Sidebar />

    <div class="main">
        <div class="container-fluid">
            <div class="row">
                <div class="col-md-6 col-sm-6">
                    this side
                    <btton class="btn btn-primary">hello</btton>
                </div>
                <div class="col-md-6 col-sm-6">
                    <img src="../assets/growth.png" alt="My Image">
                    <h5>Users</h5>

                    <img src="../assets/growth.png" alt="My Image">
                    <h5>Total Products</h5>
                </div>
            </div>

        </div>


    </div>
</template>

<script>
import Sidebar from '../views/Sidenav.vue'

export default {
    name: 'ParentView',
    components: {
        Sidebar
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

img{
    margin-top: 3%;
    height: 20%;
}
</style>