<template>
  <div class="user-detail-item flex flex-row ">
      <div class="basis-1/2 mt-32">
          <div class="flex flex-col justify-center items-center">
              <input
                  placeholder="Name.."
                  type="text"
                  class="border border-2 rounded-lg w-96 h-10 mb-10 p-1.5"
              >
              <input
                  placeholder="Password.."
                  type="date"
                  class="border border-2 rounded-lg w-96 h-10 mb-10 p-1.5"
              >
              <select v-model="cat_gender" name="genders" class="border border-2 rounded-lg w-96 h-10 mb-10 p-1.5">
                  <option v-for="gender in genders" :key="gender" :value="gender" >{{ gender }}</option>
              </select>
              <select v-model="cat_gender" name="genders" class="border border-2 rounded-lg w-96 h-10 mb-10 p-1.5">
                  <option v-for="gender in genders" :key="gender" :value="gender" >{{ gender }}</option>
              </select>
              <input
                  placeholder="Password.."
                  type="date"
                  class="border border-2 rounded-lg w-96 h-10 mb-6 p-1.5"
              >
          </div>
      </div>
      <div class="basis-1/2 mt-32">
          abc
      </div>
  </div>
</template>
<script>
export default {
    name: "UserDetailView",
    data() {
        return {
            genders:['Male','Female','Other'],
            cat_gender: ''
        }
    },
    watch: {
        cat_gender() {
            console.log(this.cat_gender)
        }
    },
    methods: {
        inputEvent() {
            console.log(this.cat_gender)
        }
    }
}
</script>

<style scoped>
.user-detail-item{
    background-color: #d7e4ea;
    height: 100vh;
}
</style>