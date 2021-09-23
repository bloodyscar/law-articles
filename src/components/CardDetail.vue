<template>
<div>
    <div class="d-flex mb-5">
        <button v-on:click="updateUser(detail.slug)" class="btn btn-sm btn-info">Edit</button>
        <button class="btn btn-sm btn-danger ml-3" v-on:click="deleteUser(detail.slug)">Delete</button>
    </div>
<div>
    <div class="text-center">
        <h2 class="font-weight-bold">
            {{ detail.title }}
        </h2>
        <p>Published on {{ detail.created_at | formatDate}} • By {{ detail.user.name }}</p>
        <p>
            <span v-for="item in detail.tags" :key="item.id">
                #{{item.name}}
            </span>
        </p>
    </div>
    <div class="card" style="overflow:hidden;">
        <div class="wrapper-image" >
            <img :src=" 'https://apilawarticlez.herokuapp.com/' + detail.thumbnail " class="img-fluid" width="100%" style="object-fit: cover; object-position: center;">
        </div>
    </div>
    <div class="mt-3 paragraf" >
        {{ detail.body }} <br>
    </div>
</div>
</div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'CardDetail',
    data(){
        return{
            detail:[],
        }
    },
    methods:{
        setDetail(data){
            this.detail = data;
        },
        deleteUser(slug){
        const token = localStorage.getItem('token')
        axios.delete('http://127.0.0.1:8000/api/article/delete/' + slug, {
        headers: {
            'Authorization': 'Bearer ' + token}
        })
            .then(() => {
                alert('Berhasil hapus Article');
                return this.$router.push('/articles');
            }).catch(e => console.log(e.message))
        },
        updateUser(slug){
            return this.$router.push('/articles/edit/'+slug)
        }
    },
    mounted(){
        axios.get('http://127.0.0.1:8000/api/show/' + this.$route.params.slug)
        .then((response) => {
            this.setDetail(response.data.data)
        })
        .catch((error) => {
            console.log(error.message);
        });
    },

}
</script>

<style>

</style>