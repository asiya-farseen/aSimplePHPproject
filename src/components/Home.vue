
<template>
<Header></Header>
<h4>Hello {{name}} , Welcome to Pateint Portal </h4>
<table border="2">
    <tr>
        <td>ID</td>
        <td>NAME</td>
        <td>ADDRESS</td>
        <td>CONTACT</td>
        <td>ACTIONS</td>

    </tr>
    <tr v-for="item in patient" :key="item.id">
    <td>{{ item.id }}</td>
    <td>{{ item.name }}</td>
    <td>{{ item.address }}</td>
    <td>{{ item.contact }}</td>
    <td><router-link :to ="'/update/'+item.id"><i class="bi bi-pencil-square"></i></router-link></td>

<td><button v-on:click="deletepateint(item.id)"><i class="bi bi-trash"></i></button></td>
    </tr>
</table>
</template>
<script>
import Header from './Header.vue';
import axios from 'axios';
export default
{
    name:'Home',
    data()
    {
return{
    name:'',
    patient:[],
}
    },
    components:{
        Header
    },
    methods:{
async deletepateint(id)
{
    let result=await axios.delete("http://localhost:3000/patients/"+id);
    if(result.status===200)
    {
        this.loadData()
    }
},
async loadData()
{
    let user=localStorage.getItem('user-info');
        this.name=JSON.parse(user).name;
        if(!user)
        {
            this.$router.push({name:'SignUp'}) 
        }
        let result=await axios.get("http://localhost:3000/patients");
        console.warn(result);
        this.patient=result.data;
}
    },
    async mounted()
    {
       this.loadData()
    }
} 
</script>
<style>
td{
    width:100px;
    height:20px;
    border:2px solid black;
    text-align: center;
    

}
</style>