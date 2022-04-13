<template>
    
    <div class="message-container-error">
        <p>{{msgErr}}</p>
        
    </div>

</template>

<script>

export default{
    name: "MessageErr",
    props:{
        msgErr: String,       
    }
}
</script>

<style scoped>
.message-container-error{
    color: #004085;
    background-color: #f5d4ae;
    border: 2px solid red;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
}

</style>
