<template>
    <Sidebar />

    <div class="main">
        <div class="container-fluid">
            <div class="row">
              <h5>Create Product</h5>
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
</style>