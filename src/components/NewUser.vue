<template>
    <div id="new-user">
        <h1>Create New User</h1>
   
         <Message :msg="msg" v-show="msg" />
         <MessageErr :msgErr="msgErr" v-show="msgErr" />
        
    </div>
   
    <div id="container-form">
        <div class="btn-back">
            <button id="btn-back" class="btn-default" @click="GotoBackList()">Back to List</button>
        </div>

        <form id="create-user-form" @submit="createUser">
            <div class="input-container">
              <label for="nome">First Name *</label>
              <input type="text" id="firstName" name="firstName" v-model="firstName" placeholder="First Name" />

            </div>

             <div class="input-container">
              <label for="nome">Last Name *</label>
              <input type="text" id="lastName" name="lastName" v-model="lastName" placeholder="Last Name" />

            </div>

              <div class="input-container">
                <label for="nome">E-mail *</label>
                <input type="text" id="email" name="email" v-model="email" placeholder="E-mail" />

              </div>

              <div class="input-container">
                <label for="nome">Phone Number *</label>
                <input type="text" id="phoneNumber" name="phoneNumber" v-model="phoneNumber" placeholder="Phone Number" />

              </div>
              
              <div class="input-container">
                <label for="role">Role *</label>
               
                <select name="role" id="role" v-model="role">
                    <option value="-1" selected>None</option>
                    <option value="1">Administrator</option>
                    <option value="2">Manager</option>
                </select>
              </div>

              <div class="input-container">
                  <input type="submit" class="submit-btn" value="Save" />
              </div>

        </form>

    </div>


</template>

<script>
import Message from "./Message.vue";
import MessageErr from "./MessageErr.vue";

export default{

    name:"NewUser",
    data(){
      return{
        firstName: "",
        lastName: "",
        email: "",
        phoneNumber: "",
        role: null,
        status: false,
        msg: null,
        msgErr: null

      };
    },
    components: {
      Message,
      MessageErr
    },
    methods:{
      GotoBackList(){
        this.$router.push('/users'); 
      },
      async createUser(e){
        e.preventDefault();

        const data = {
          FirstName: this.firstName,
          LastName: this.lastName,
          UserName: this.email,
          PhoneNumber: this.phoneNumber,
          UserRoleId: this.role,
          ClientIP: null,
          UserLog: { UserId: 0,  ApplicationVersion: "1.0.0",   DeviceId: 1, DeviceName: "Chrome",  DeviceVersion: "100",
                     DevicePlatform: "Windows 10", DeviceLatitude: null, DeviceLongitude: null, IP: null 
          } 
         
        }

        const requestModel = JSON.stringify(data);
        var token = JSON.parse(localStorage.getItem( 'token'));
      
        const req = await fetch('https://localhost:44325/User', {
            method: "Post",
            headers: { "Content-Type": "application/json",
                       "Authorization": token,
            },
            body: requestModel,
            Authorization: token,
        });

      const resp = await req.json();

      this.status = resp.Success;
      if(this.status)
        this.msg = `User Created success!`;
      else
        this.msgErr = `Error Creating user!`;

      this.ClearMessage();

      },
       async ClearMessage(){
        setTimeout(() => (this.msg = "",this.msgErr = ""), 3000);
    }

  }
   
}

</script>

<style scoped>

.btn-back #btn-back{
    display: flex;
    float: right;
}

.input-container{
  display: inline-grid;
  flex-direction: row;
  margin-bottom: 20px;
  padding: 5px;
}

.input-container #phoneNumber, #role{
  width: 455px;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
  color: #222;
  padding: 5px 5px;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

.submit-btn {
    background-color: blue;
    color: white;
    font-weight: bold;
    border: 1px solid blue;
    border-radius: 3px;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .3s;
    width: 100px;
}

.submit-btn:hover {
  background-color: #1a53ff;

}

</style>




