<template>
    <img class="logo" alt="Vue logo" src="https://res.cloudinary.com/ravikiran143/image/upload/v1641196519/sc-logo_p7kdtx.png">
    <h1>SignUp</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name" />
        <input type="text" v-model="email" placeholder="Enter Mail" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="signUp">SignUp</button>
        <p>
            <router-link to='/login' >Login</router-link>
        </p>
    </div>

</template>
<script>
    import axios from 'axios'
    export default {
        name:'Signup',
        data()
        {
            return {
                name:'',
                email:'',
                password:''
            }
        },
        methods:{
            async signUp(){
              let result = await axios.post("http://localhost:3000/user",{
                  email:this.email,
                  password:this.password,
                  name:this.name
              });
              console.warn(result);
              if(result.status==201){
                //   alert("sign-up-done");
                  localStorage.setItem("user",JSON.stringify(result.data))
                this.$router.push({name:'Home'})
                }
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
    .register input {
        width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid skyblue;
    }
    .register button {
        width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    background-color: lightblue; 
    cursor: pointer;
    }
</style>