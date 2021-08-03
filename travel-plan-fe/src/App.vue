<template>
  <div id="app">
    <div class="container">
      <Header :title="headerTitle" />
      <UserForm v-show="showUser" @display-data="displayDetails($event)" />
      <DisplayUser v-show="!showUser" :users="userdata" @btn-click="onBack" />
    </div>
  </div>
</template>

<script>
import Header from './components/header.vue'
import UserForm from './components/userform.vue'
import DisplayUser from './components/displayuser.vue'

export default {
  name: 'App',
  components: {
    Header,
    UserForm,
    DisplayUser,
  },

  data() {
    return {
      userdata: [],
      name:'',
      email: '',
      country: '',
      user: {},
      showUser: true,
      headerTitle: "Explore the World!",
    }
  },

  methods: {
    displayDetails(newUser) {
      console.log("User Data : " + JSON.stringify(newUser));
      this.userdata = [...this.userdata, newUser]
      this.showUser = !this.showUser;
      this.headerTitle = this.showUser ? "Explore the World!" : "Traveller Details"
      console.log("User Data :: " + JSON.stringify(this.userdata));
    },

    onBack() {
      this.showUser = !this.showUser;
      this.headerTitle = this.showUser ? "Explore the World!" : "Traveller Details"
    }
  },

  created() {
    this.userdata = [
      {
      name: "Vinay",
      email: "vinaya@gmail.com",
      country: "india",
      numberOfTravellers: 4,
      budget: 4000
    }
    ]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
</style>