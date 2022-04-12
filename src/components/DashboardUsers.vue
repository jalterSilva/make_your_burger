<template>

    <div class="user-filters">
         <div class="input-container">
            <label for="nome">First Name: </label>
            <input
                type="text"
                name="firstName"
                v-model="firstName"
                placeholder="first name"
            />

         </div>

          <div class="input-container">
            <label for="nome">Last Name: </label>
            <input
                type="text"
                name="lastName"
                v-model="lastName"
                placeholder="last name"
            />

         </div>

        <div class="search-div">
            <button class="btn-default" @click="getAllUsers()">Search</button>
        </div>
         <div class="new-user-div">
             <button id="new-user" class="btn-default" @click="CreateUser()">+ New User</button>
        </div>
       
   
    </div>

   <div id="user-table">
       <!-- cols -->
       <div>
           <div id="user-table-heading">
               <div class="user-id">#:</div>
               <div>First Name</div>
               <div>Last Name</div>
               <div>E-mail</div>
               <div>Phone number</div>
               <div>Status</div>
           </div>
       </div>
        <!-- rows -->
        <div id="user-table-rows">
          <div class="user-table-row" v-for="user in users" :key="user.Id">
              <div class="order-number">{{user.Id}}</div>
              <div>{{user.FirstName}}</div>
              <div>{{user.LastName}}</div>
              <div>{{user.UserName}}</div>
              <div>{{user.PhoneNumber}}</div>
              <div>{{user.Active}}</div>

          </div>

        </div> 
   </div>

</template>

<script>
export default {
    name: "DashboardUsers",
    data(){
        return {
            users: [],
            firstName: "",
            lastName: "",    
           
        }
    },
    methods: {   
        async getAllUsers(){
            //let token = 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJVc2VySWQiOiI0IiwiVXNlck5hbWUiOiJqYWx0ZXIuZGFzaWx2YUBzdGdlbi5jb20iLCJGaXJzdE5hbWUiOiJKYWx0ZXIiLCJMYXN0TmFtZSI6ImRhIFNpbHZhIiwiQ3VycmVudEhlcmRDb2RlIjoiOTkwMTAxOTciLCJGYXJtSWQiOiI5OTAxMDE5NyIsIkhlcmRDb2RlIjoiOTkwMTAxOTciLCJGYXJtTmFtZSI6IlNhcmEncyBUZXN0IEhlcmQiLCJGYXJtT3duZXJOYW1lIjoiU2FyYSdzIFRlc3QgSGVyZCIsIkZhcm1DaXR5IjoiVmFpbCIsIkZhcm1TdGF0ZSI6IkFaIiwiRmFybUNvdW50cnkiOiJVbml0ZWQgU3RhdGVzIiwiRmFybUVtYWlsIjoiIiwiVXNlclJvbGVJZCI6IjEiLCJodHRwOi8vc2NoZW1hcy5taWNyb3NvZnQuY29tL3dzLzIwMDgvMDYvaWRlbnRpdHkvY2xhaW1zL3JvbGUiOiJBZG1pbmlzdHJhdG9yIiwianRpIjoiODRlNmE3NTItNGQwMy00YWM4LTlhMmUtOTIzYTdhYmZkZjI5IiwiZXhwIjoxNjQ5OTM2Mzk5fQ.MPUrvt52y-vx8k4UsQ3cHpk0ZDhQTUhG-S9MKIDZh9k';        
            //  localStorage.setItem( 'token', JSON.stringify(token) );

            var token = JSON.parse(localStorage.getItem( 'token'));

            const req = await fetch(`https://localhost:44325/User?firstName=${this.firstName}&lastName=${this.lastName}`, {
                method: 'GET',
                headers: {
                    Accept: 'application/json',
                    Authorization: token,
                }
            });

            const data = await req.json();
            this.users = data.ResultData; 
        },
        CreateUser(){
             this.$router.push('/users/CreateUser'); 
        }
    },
    mounted(){
        this.getAllUsers();
  
    }
   
}

</script>

<style scoped>
#user-table{
    max-width: 1200px;
    margin: 0 auto;
}

#user-table-heading,
#user-table-rows,
.user-table-row{
    display: flex;
    flex-wrap: wrap;

}

#user-table-heading{
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}

#user-table-heading div,
.user-table-row div {
    width: 19%;

}

.user-table-row{
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
}

#user-table-heading .user-id,
 .user-table-row .order-number{
     width: 5%;
}

input,
select {
  padding: 5px 10px;
  width: 200px;
}

/* filters */
.input-container{
width: 25%;
display: inline;
padding-left: 15px;

}

.user-filters{
    max-width: 1200px;
    margin: auto;
    margin-bottom: 20px;
}

.search-div{
    display: inline-block;
    padding-left: 15px;
}

.new-user-div{
    display: inline-flex;
    width: 40%;
}

</style>
