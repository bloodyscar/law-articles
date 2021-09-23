<template>
    <section class="highlight" data-aos="zoom-in" data-aos-delay="150">
        <div class="container">
            <div class="row">
                <div class="col">
                    <h2 class="font-weight-bold">Our Highlight</h2>
                </div>
            </div>
            <div class="row">
                <div class="col-md-4" v-for="article in articles" :key="article.id">
                    <Card :article="article"/>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import Card from '@/components/Card.vue'
import axios from 'axios';
export default {
    name: 'Highlight',
    components:{
        Card
    },
    data(){
        return{
            articles: [],
        }
    },
    methods:{
        setArticles(data){
            this.articles = data;
        }
    },
    mounted(){
        axios.get('https://apilawarticlez.herokuapp.com/api/articles')
        .then(response => this.setArticles(response.data.data) )
        .catch(error => console.log(error.message))
    }
}
</script>

<style>

</style>