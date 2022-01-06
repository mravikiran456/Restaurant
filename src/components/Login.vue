<template>
    <img class="logo" alt="Vue logo" src="https://res.cloudinary.com/ravikiran143/image/upload/v1641196519/sc-logo_p7kdtx.png">
    <h1>Login</h1>
    <div class="login">
        <input type="text" v-model="email" placeholder="Enter Mail" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="login">Login</button>
        <p>
            <router-link to='/sign-up' >Signup</router-link>
        </p>
    </div>
</template>

<script>
    import axios from 'axios'
   export default {
       name:"Login",
       data() {
           return{
               email:'',
               password:''
           }
       },
       methods:{
          async login()
           {
               let result=await axios.get(
                   `http://localhost:3000/user?email=${this.email}&password=${this.password}`
               )
               if(result.status==200 && result.data.length>0){
                //   alert("sign-up-done");
                  localStorage.setItem("user",JSON.stringify(result.data[0]))
                this.$router.push({name:'Home'})
               }
               console.warn(result)
           }

       },
       mounted()
        {
            let user =localStorage.getItem('user');
            if(user){
                this.$router.push({name:'Home'})
            }
        }
   } 
</script>
<style>
    .logo{
width: 100px;
height: 100px;
    }
    .login input{
        width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid skyblue;
    }
    .login button{
        width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    background-color: lightblue; 
    cursor: pointer;
    }
</style>