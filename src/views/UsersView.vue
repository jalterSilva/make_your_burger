<template>
    <div class="main-container">
        <h1>Users</h1>
        <DashboardUsers/>
        
    </div>
</template>

<script>
import DashboardUsers from '../components/DashboardUsers.vue'

    export default {
        name: "Users",
        components:{
            DashboardUsers
        }
    }
</script>

<style scoped>

</style>
