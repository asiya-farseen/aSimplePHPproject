
<template>
    <Header></Header>
    <h1>UPDATE</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter name" v-model="patient.name" />
        <input type="text" name="address" placeholder="Enter address" v-model="patient.address" />
        <input type="text" name="contact" placeholder="Enter contact" v-model="patient.contact" />
        <button type="button" v-on:click="updatePatient">update patient</button>

    </form>
</template>
<script>
import Header from './Header.vue';
import axios from 'axios';
export default
    {
        name: 'Update',
        components: {
            Header
        },
        data() {
            return {
                patient:
                {
                    name: '',
                    address: '',
                    contact: '',
                }
            }
        },
        methods:
        {
            async updatePatient()
             {
                console.warn(this.patient)
               const result = await axios.put("http://localhost:3000/patients/" + this.$route.params.id, {
                 name: this.patient.name,
                     address: this.patient.address,
                     contact: this.patient.contact,

                });
                 if (result.status == 200) {
                     this.$router.push({ name: 'Home' })

               }
             }
        },
        async mounted() {
            let user = localStorage.getItem('user-info');
            if (!user) {
                this.$router.push({ name: 'SignUp' })
            }
            const result = await axios.get('http://localhost:3000/patients/' + this.$route.params.id)
            // console.warn(this.$route.params.id)
            console.warn(result.data)
            this.patient = result.data
        }
    }
</script>