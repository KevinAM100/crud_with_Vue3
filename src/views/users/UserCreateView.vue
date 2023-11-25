<script>
import axios from 'axios';


export default {
    name: "UserCreateView",
    data(){
        return{
            model:{
                user:{
                    username: '',
                    password: '',
                    email: '',
                    firstName: '',
                    lastName: '',
                    age: '',
                    birthDay: ''
                }
            }
        }
    },
    methods:{
        saveUser(){
            axios.post('http://localhost:8080/v1/users', this.model.user)
            .then(res => {
                alert('users was saved successful');
                this.model.user = {
                    username: '',
                    password: '',
                    email: '',
                    firstName: '',
                    lastName: '',
                    age: '',
                    birthDay: ''
                }
            }).catch(function (error){

            })
        }
    }
}

</script>

<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Add User</h4>
            </div>
            <div class="card-body">
                <div class="mb-3">
                    <label for="">UserName</label>
                    <input type="text" v-model="model.user.username" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">Password</label>
                    <input type="text" v-model="model.user.password" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">Email</label>
                    <input type="text" v-model="model.user.email" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">First Name</label>
                    <input type="text" v-model="model.user.firstName" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">Last Name</label>
                    <input type="text" v-model="model.user.lastName" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">Age</label>
                    <input type="text" v-model="model.user.age" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">Birth Day</label>
                    <input type="text" v-model="model.user.birthDay" class="form-control">
                </div>
                <div>
                    <button type="button" @click= "saveUser" class="btn btn-primary">
                        save
                    </button>&nbsp;
                    <RouterLink to="/users" class="btn btn-primary">
                         Back
                    </RouterLink>

                </div>

            </div>
            
        </div>

    </div>
</template>

<style scoped>

</style>