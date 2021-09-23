<template>
    <div class="d-flex justify-content-center align-items-center" style="height:100vh; background-color: #664200;">
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <div class="card">
                        <div class="card-body">
                            <form action=""  @submit.prevent="setLogin">
                                <div class="form-group">
                                    <label for="email">Email</label>
                                    <input type="email" v-model="login.email"  class="form-control"/>
                                </div>
                                <div class="form-group">
                                    <label for="password">Password</label>
                                    <input type="password" v-model="login.password" class="form-control"/>
                                </div>
                                <button type="submit" class="btn btn-primary">Login</button>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'LoginPage',
    data(){
        return{
            login:{
                email: '',
                password: '',
            }
        }
    },
    methods:{
        setLogin(){
            axios.post('http://127.0.0.1:8000/api/login', this.login)
            .then((response) => {
                localStorage.setItem('token', response.data.token)
            })
        }
    }
}
</script>

<style>

</style>