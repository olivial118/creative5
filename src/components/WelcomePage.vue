<template>
  <div class="column">
    <h1>Journey of Your LIfe</h1><br>
    <h2>Journal writing is a Voyage to the interior</h2>
    <form v-on:submit.prevent="register">
      <p>Create an account for your Journey with us.<br>
          Only you can access your journal with ID.</p>
      <input class="narrow" v-model="username" placeholder="User Name">
      <input class="narrow" v-model="name" placeholder="First and Last Name"><br/> 
      <input class="narrow" v-model="email" placeholder="Email Address">
      <input class="narrow" type="password" v-model="password" placeholder="Password"><br/>
      <button class="alternate" type="submit">Register</button>
    </form>
    <p class="error">{{registerError}}</p>
  </div>
</template>

<script>
 export default {
   name: 'WelcomePage',
   data () {
     return {
       username: '',
       email: '',
       password: '',
       name: '',
     }
   },
   computed: {
     registerError: function() {
       return this.$store.getters.registerError;
     },
   },
   methods: {
     register: function() {
       this.$store.dispatch('register',{
 username: this.username,
         email: this.email,
         password: this.password,
 name: this.name,
       });
     }
   }
 }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

 h1 {
     margin-bottom: 0px;
     color: white;
 }
 h2 {
     margin-top: 0px;
     font-size: 1.2em;
     font-weight: normal;
     margin-bottom: 50px;
     color: white;
 }
 p {
    color: white;
}
 .narrow {
     width: 170px;
     border-radius: 15px;
 }
 .wide {
     width: 370px;
 }
 .alternate {
     background-color: black;
}
</style>
