<template>
    <div>
        <div class="sidebar">
            <h5 class="font-weight-bold mb-2">More Articles</h5>
            <span style="font-size: 0.8em;">
                <a href="" v-for="item in articles" :key="item.id">
                    {{ item.title }} <br><hr>
                </a>
            </span>
        </div>
        <div class="mt-4">
            <h5 class="font-weight-bold">Legal Services</h5>
            <span style="font-size: 0.8em;"><a href="">
                Legality
            </a></span>
            <hr>
            <span style="font-size: 0.8em;"><a href="">
                Franchise Conctact
            </a></span>
            <hr>
            <span style="font-size: 0.8em;"><a href="">
                Company Acquisition
            </a></span>
            <hr>
        </div>
        <div class="mt-5">
            <h5 class="font-weight-bold mb-3">Tag</h5>
            <span class="mt-3" style="font-size: 0.8em;">
                <a href="" v-for="tag in tags" :key="tag.id">
                    {{tag.name}} <br><hr>
                </a
            ></span>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Sidebar',
    props:['item'],
    data(){
        return {
            tags: [],
            articles:[],
        }
    },
    methods: {
        setTags(data){
            this.tags = data;
        },
        setArticles(data){
            this.articles = data;
        }
    },
    mounted(){
        // get Tags 
        axios.get('http://127.0.0.1:8000/api/tags')
        .then((response) => {
            this.setTags(response.data.data);
        })
        .catch((error) => {
            console.log(error.message);
        });

        // get Title 
        axios.get('http://127.0.0.1:8000/api/articles'  )
        .then((response) => {
            this.setArticles(response.data.data);
        })
        .catch((error) => {
            console.log(error.message);
        });
    }
}
</script>

<style>

</style>