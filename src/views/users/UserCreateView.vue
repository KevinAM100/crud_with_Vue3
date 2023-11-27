<script setup>
import axios from 'axios';
import {reactive, computed} from 'vue'; 
import useVuelidate from '@vuelidate/core'; 
import {required, email, minLength, maxLength, helpers} from '@vuelidate/validators';

const model = reactive({
    user:{
                    username: '',
                    password: '',
                    email: '',
                    firstName: '',
                    lastName: '',
                    age: '',
                    birthDay: ''
                }
});

const containsUser = (value) =>{
    return value.includes("user");
}

const rules = computed(() =>{
    return{
        user:{
                    username: {required,
                         minLength: minLength(3),
                          maxLength: maxLength(15),
                        },
                    password: {required},
                    email: {required, email},
                    firstName: {required, 
                         minLength: minLength(3),
                          maxLength: maxLength(8)},
                    lastName: {required, 
                         minLength: minLength(5),
                          maxLength: maxLength(15)},
                    age: {required},
                    birthDay: {required}
                }
    }
})

const v$ = useVuelidate(rules, model);

     const   saveUser = async() => {
            const confirm = await v$.value.$validate();
            if(confirm){
                axios.post('http://localhost:8080/v1/users', model.user)
            .then(res => {
                alert('users was saved successful');
                model.user = {
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
            } else{
                alert("error, form not submitted!")
            }
            
        };
    


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
                    <input type="text" v-model=" model.user.username" class="form-control">
                    <span v-for=" error in v$.user.username.$errors" :key="error.$uid" class="text-red-500">{{error.$message}}</span>  
                </div>
                
                <div class="mb-3">
                    <label for="">Password</label>
                    <input type="text" v-model="model.user.password" class="form-control">
                    <span v-for=" error in v$.user.password.$errors" :key="error.$uid" class="text-red-500">{{error.$message}}</span>
                </div>
                <div class="mb-3">
                    <label for="">Email</label>
                    <input type="text" v-model="model.user.email" class="form-control">
                    <span v-for=" error in v$.user.email.$errors" :key="error.$uid" class="text-red-500">{{error.$message}}</span>
                </div>
                <div class="mb-3">
                    <label for="">First Name</label>
                    <input type="text" v-model="model.user.firstName" class="form-control">
                    <span v-for=" error in v$.user.firstName.$errors" :key="error.$uid" class="text-red-500">{{error.$message}}</span>
                </div>
                <div class="mb-3">
                    <label for="">Last Name</label>
                    <input type="text" v-model="model.user.lastName" class="form-control">
                    <span v-for=" error in v$.user.lastName.$errors" :key="error.$uid" class="text-red-500">{{error.$message}}</span>
                </div>
                <div class="mb-3">
                    <label for="">Age</label>
                    <input type="text" v-model="model.user.age" class="form-control">
                    <span v-for=" error in v$.user.age.$errors" :key="error.$uid" class="text-red-500">{{error.$message}}</span>
                </div>
                <div class="mb-3">
                    <label for="">Birth Day</label>
                    <input type="text" v-model="model.user.birthDay" class="form-control">
                    <span v-for=" error in v$.user.birthDay.$errors" :key="error.$uid" class="text-red-500">{{error.$message}}</span>
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