<template>
  <section class="section-update" data-aos="zoom-in" data-aos-delay="100">
        <div class="container">
            <div class="row">
                <div class="col">
                    <h2 class="font-weight-bold">Latest Update</h2>
                </div>
            </div>
            <div class="row mt-3 d-flex justify-content-end" >
                <div class="col-md-6">
                    <div class="card" style="overflow:hidden;">
                        <div class="wrapper-image" >
                            <img :src=" 'http://127.0.0.1:8000/storage/' + article.thumbnail " class="img-fluid" width="100%" style="max-height: 350px;">
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <h2 class="font-weight-bold" >{{ article.title }}</h2>
                    <p class="mt-4">{{ article.body.substring(0,450) + "..." }}</p>
                    <router-link :to=" '/articles/' +article.slug ">Read More</router-link>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import axios from 'axios'
export default {
    name: 'LatestUpdate',
    data(){
        return{
            article: [],
        }
    },
    methods:{
        setArticles(data){
            this.article = data;
        }
    },
    mounted(){
        axios.get('http://127.0.0.1:8000/api/show/quo-vadis-perlindungan-konsumen-indonesia')
        .then((response) => {
            this.setArticles(response.data.data)
        })
        .catch((error) => {
            console.log(error.message);
        })
    }
}
</script>

<style>

</style>