<template>
  <div class="image-cat">
      <router-link to="/">
          <div
              class="nav-logo ml-3.5 absolute mr-3.5 text-3xl text-white font-extrabold"
          >
              Brindr
          </div>
      </router-link>
      <div class="login-form absolute rounded flex flex-col justify-center items-center">
          <div>
              <h1 class="font-bold mb-12 text-xl mt-3">
                  SIGN IN
              </h1>
          </div>
          <div class="flex flex-col justify-center items-center p-10">
              <input
                  v-model="model.email"
                  placeholder="Email.."
                  type="text"
                  class="border border-2 rounded-lg w-96 h-10 mb-6 p-1.5"
              >
              <input
                  v-model="model.password"
                  @keydown.enter="signIn"
                  placeholder="Password.."
                  type="password"
                  class="border border-2 rounded-lg w-96 h-10 mb-6 p-1.5"
              >
              <div>
                  <div class="font-bold forgot-item">
                      <router-link to="#">
                          Forgot Password?
                      </router-link>
                  </div>
              </div>
              <button
                  class="w-64 h-10 text-center border rounded-lg border-4 login-button"
                  type="submit"
                  @click="signIn"
              >
                  LOGIN
              </button>
              <div class="mt-3 flex flex-col items-center">
                  <p>
                      Don't have an account?
                  </p>
                  <router-link class="font-bold register-item" to="/register">
                      Register
                  </router-link>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
    name: "LoginView",
    data() {
      return {
          model: {
              email:'',
              password:''
          }
      }
    },
    methods: {
        signIn() {
            axios.post('http://localhost:8000/login', {
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
        }
    }
}
</script>

<style scoped>
.image-cat{
    background-image: url("../assets/cats-wallpaper-desktop-thumbnail-1.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    height: 100vh;
    position: relative;
}
.login-form {
    height: 100vh;
    width: 40vw;
    left:0;
    background-color: #d7e4ea;
}
.login-button {
    background-color: white;
    border-color: #6096B4;
    color: #6096B4;
}
.login-button:hover {
    background-color: #6096B4;
    border-color: #6096B4;
    color: white;
}
input {
    border-color: #6096B4;
}
.nav-logo {
    right:0.5%;
    top:2%;
}
</style>