<template>
  <div v-if="!sessionStorageUserId" class="image-item">
    <div class="flex nav-logo ml-3.5 absolute text-3xl text-white font-extrabold">
        Brindr</div>
    <router-link :to="{ name:'login'}" >
        <button class="nav-button bg-white py-2 px-6 mr-3.5 rounded-xl absolute font-bold">Login</button>
    </router-link>

    <div class="absolute swipe-items">
        <div class="mb-10 text-white font-extrabold text-3xl">SWIPE RIGHT</div>
        <router-link :to="{ name:'register'}" >
            <button class="button-item text-white p-3 rounded-2xl">REGISTER</button>
        </router-link>
    </div>
  </div>
  <div v-if="sessionStorageUserId">
    ABC
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: 'HomeView',
  data() {
      return {
          sessionStorageUserId: '',
      }
  },
  created() {
      this.getSessionStorageUserId()
      this.getUserDetail()
  },
  methods: {
      getSessionStorageUserId() {
        this.sessionStorageUserId = sessionStorage.getItem('userId')
      },
      getUserDetail() {
          if(this.sessionStorageUserId) {
              axios.get(`http://localhost:8000/user` ,{
                  params: {
                      userId : this.sessionStorageUserId
                  }
              }).then(response => {
                  console.log(response.data)
              }).catch(response => {
                  console.log(response)
              })
          }
      }
  }
}
</script>
<style scoped>
#nav-item {
    height: 10vh;
    //background-color: #6096B4;
    top: 0;
    width: 100vw;
    opacity:0;
}
.nav-button {
    right:0.5%;
    top:2%;
    color: #6096B4;
}
.nav-button:hover {
    color: white;
    background-color: #6096B4;
}
.nav-logo {
    left:0.5%;
    top:2%;
}
.image-item {
    background-image: url("../assets/cats-wallpaper-desktop-thumbnail-11.jpg");
    background-size: cover; 
    background-repeat: no-repeat;
    height: 100vh;
    position: relative;
}
.swipe-items {
    top: 50%;
    right: 30%;
}
.button-item{
    background-color: #6096B4;
}
.button-item:hover{
    background-color: white;
    color: #6096B4;
}
</style>
