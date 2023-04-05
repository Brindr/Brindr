<template>
  <div class="image-cat">
      <router-link to="/">
          <div
              class="nav-logo ml-3.5 absolute text-3xl text-white font-extrabold"
          >
              Brindr
          </div>
      </router-link>
      <div class="register-form absolute p-20">
          <div>
              <h1 class="font-bold mb-12 text-xl">REGISTER</h1>
          </div>
          <div class="flex flex-col items-center ">
              <div class="flex flex-col items-center justify-center">
                  <input
                      placeholder="Email.."
                      class="border border-2 rounded-lg w-96 h-10 mb-6 p-1.5"
                      type="email"
                      v-model="model.email"
                  />
                  <input
                      placeholder="Password.."
                      class="border border-2 rounded-lg w-96 h-10 mb-6 p-1.5"
                      type="password"
                      v-model="model.password"
                  />
                  <input
                      placeholder="Confirm Password.."
                      class="border border-2 rounded-lg w-96 h-10 p-1.5"
                      :class="[!errorMessageActive ? 'mb-6' : 'mb-0']"
                      type="password"
                      v-model="model.confirmationPassword"
                  />
              </div>
              <button
                  class="button-item w-64 h-10 text-center border border-4 rounded-lg "
                  type="submit"
                  @click="submitUser"
              >
                  REGISTER
              </button>
              <div class="mt-3 flex flex-col items-center">
                  <p>
                      Already have an account?
                  </p>
                  <router-link class="font-bold underline sign-item" to="/login">
                      Sign In
                  </router-link>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
    name:"RegisterView",
    data() {
        return {
            model: {
                email: '',
                password: '',
                confirmationPassword: ''
            }
        }
    },
    created() {

    },
    methods: {
        submitUser() {
            axios.post('http://localhost:8000/signup',{
                email: this.model.email,
                password: this.model.password,
            }).then(response => {
                sessionStorage.setItem("userId", `${response.data.userId}`);
                this.getUserDetail()
            }).catch(response => {
                console.log(response)
            })
        },
        getUserDetail() {
            if(sessionStorage.getItem('userId')) {
                axios.get(`http://localhost:8000/user` ,{
                    params: {
                        userId : sessionStorage.getItem('userId')
                    }
                }).then(response => {
                    if(response.data.first_name) {
                        this.$router.push({name: 'home'})
                    }else{
                        this.$router.push({name: 'userDetail'})
                    }
                }).catch(response => {
                    console.log(response)
                })
            }
        },
    },
    computed: {

    }
}
</script>

<style scoped>
.image-cat{
    background-image: url("../assets/cats-wallpaper-desktop-thumbnail-7.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    height: 100vh;
    position: relative;
}
.register-form{
    right:0;
    height: 100vh;
    background-color: #d7e4ea;
    width:40vw;
}
.button-item{
    background-color: white;
    border-color: #6096B4;
    color: #6096B4;
}
.button-item:hover {
    background-color: #6096B4;
    border-color: #6096B4;
    color: white;
}
input{
    border-color: #6096B4;
}
.nav-logo {
    left:0.5%;
    top:2%;
}
</style>
