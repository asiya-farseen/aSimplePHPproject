<template>
    <div class="nav">
        <router-link to="/">HOME</router-link>
        <router-link to="/add">ADD PATIENT</router-link>
     
        <a v-on:click="logout" href="#">LOGOUT</a>
    </div>
</template>
<script>
export default{
    name:'Header',
    methods:{
        logout()
        {
            localStorage.clear();
            this.$router.push({name:'Login'})
           // console.warn("logout")
        }
    }
}</script>
<style>
.nav{
    background-color: #333;
    overflow: hidden;
    
}
.nav a{
    float:left;
    color:gainsboro;
    padding:14px 16px;
    font-size:17px;
    text-align: center;
    text-decoration: none;
    margin-right:5px;

}
.nav a:hover{
    background:#ddd;
    color:#333;
}</style>