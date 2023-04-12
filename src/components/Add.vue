
<template>
    <Header></Header>
    <h4>WELCOME TO ADD PATEINT PAGE</h4>
    <form class="add">
        <input type="text" name="name" placeholder="Enter name" v-model="patient.name"/>
        <input type="text" name="address" placeholder="Enter address" v-model="patient.address"/>
        <input type="text" name="contact" placeholder="Enter contact" v-model="patient.contact"/>
        <button type="button" v-on:click="addPatient">Add new patient</button>

    </form>
    </template>
    <script>
    import Header from './Header.vue';
    import axios from 'axios';
    export default
    {
        name:'Add',
        components:{
            Header
        },
        data()
        {

        
        return {
            patient:
            {
name:'',
address:'',
contact:'',
            }
        }
        },
        methods:
        {
           async addPatient()
            {
                console.warn(this.patient)
                const result=await axios.post("http://localhost:3000/patients",{
                    name:this.patient.name,
                    address:this.patient.address,
                    contact:this.patient.contact,

                });
                if(result.status==201)
                {
                    this.$router.push({name:'Home'}) 
            
                }
                console.warn("result",result)
            }
        },
        mounted()
        {
            let user=localStorage.getItem('user-info');
            if(!user)
            {
                this.$router.push({name:'SignUp'}) 
            }
        }
    } 

    </script>