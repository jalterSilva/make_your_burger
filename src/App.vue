<template>
  <NavBar :logo="logo_src" :alt="app_name"/>
  <router-view />
  <Footer />
</template>

<script>
import NavBar from './components/NavBar.vue';
import Footer from './components/Footer.vue';

export default {
  components: {
    NavBar,
    Footer
  },
  data(){
    return {
      logo_src: "/img/logo.png",
      app_name: "Make Your Burger"
    }
  }
};
</script>

<style>
*{
  font-family: Helvetica;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#container-form{
 max-width: 1400px;
  margin: 0 auto;

}

#create-user-form, #edit-user-form{
  max-width: 1000px;
  margin: 0 auto;
  margin-top: 40px;

}

.main-container{
  margin: 50px;
  min-height: 250px;
}

h1{
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}

.btn-default {
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
  
}

.btn-default:hover, .btn-default-edit:hover {
  background-color: transparent;
  color: #222;
}

.btn-default-edit {
    background-color: green;
    color: white;
    font-weight: bold;
    border: 1px solid green;
    border-radius: 3px;
    padding: 8px;
    font-size: 12px;
    margin: 0 auto;
    cursor: pointer;
    transition: .3s;
}

</style>

