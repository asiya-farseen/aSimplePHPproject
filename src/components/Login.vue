<template>
    <div class="login">
        <img class="logo" src="../assets/logo.png"/>
    <h1>LOGIN</h1>
        <input type="text" v-model="email"  placeholder="Enter email"/>
        <input type="password" v-model="password"  placeholder="Enter password"/>
        <button v-on:click="login">LOGIN</button>
        <p>
            <router-link to="/sign-up">SIGNUP</router-link>
        </p>
        </div>
</template>
<script>
import axios from 'axios'
export default{
    name:'Login',
    data()
    {
      return {
        email:'',
        password:''
      }  
    },
    methods:
    {
       async login()
        {
            let result=await axios.get(
                `http://localhost:3000/users?email=${this.email}&password=${this.password}`
            )
            if(result.status==200 && result.data.length>0)
            {
                localStorage.setItem("user-info",JSON.stringify(result.data[0]))
                this.$router.push({name:'Home'})
            }
           console.warn(result)
        
        }
    },
    mounted()
    {
        let user=localStorage.getItem('user-info');
        if(user)
        {
            this.$router.push({name:'Home'}) 
        }
    }

};
</script>