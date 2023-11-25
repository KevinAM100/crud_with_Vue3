<script>
import axios from "axios";

export default {
    name: "UserView",
    data(){
        return{
            users: []
        }
    },
    methods: {
        getUsers() {
             axios.get('http://localhost:8080/v1/users?detailed=yes').then(res=>{console.log(res);
                this.users = res.data;
            }).catch(function (error){

            })   
         },
         deleteUserById(userID){
            if (confirm('Are you sure, you want to delete  this User?')){
                axios.delete(`http://localhost:8080/v1/users/${userID}`)
                .then(res=>{console.log(res);
                this.getUsers();
            }).catch(function (error){

            })   
            }
         }
    },
    mounted(){
        this.getUsers();
    }
}

</script>

<template>
    <div class="users">
        <div class="card">
            <div class="card-header">
                <h4>
                    Users
                    <RouterLink to="/users/create" class="btn btn-primary float-end">
                        Add Users
                    </RouterLink>
                </h4>
            </div>
            <div class="card-body">
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <th>Nro.</th>
                            <th>UserName</th>
                            <th>FirstName</th>
                            <th>LastName</th>
                            <th>UserDetailId</th>
                            <th>Email</th>
                            <th>Age</th>
                            <th>BirthDay</th>
                            <th>CreatedAt</th>
                            <th>Actions</th>

                        </tr>
                    </thead>
                    <tbody  v-if="users.length > 0">
                        <tr v-for="(users, index) in this.users" :key="index">
                            <td>{{ index + 1 }}</td>
                            <td>{{ users.username}}</td>
                            <td>{{ users.firstName }}</td>
                            <td>{{ users.lastName }}</td>
                            <td>{{ users.userDetailId }}</td>
                            <td>{{ users.email }}</td>
                            <td>{{ users.age }}</td>
                            <td>{{ users.birthDay }}</td>
                            <td>{{ users.createdAt }}</td>
                            <td>
                                <RouterLink :to="{ path: '/users/' + users.id + '/edit' }" class="btn btn-success">
                                             Edit
                                </RouterLink>
                                <button type="button" @click="deleteUserById(users.id)" class="btn btn-danger">
                                         Delete
                                 </button>
                            </td>

                        </tr>
                    </tbody>
                    <tbody v-else>
                        <tr>
                            <td colspan="10">
                                there are no Users
                            </td>
                        </tr>

                    </tbody>
                </table>
            </div>
        </div>
    </div>
<h1>List Users</h1>
</template>

<style scoped>

</style>