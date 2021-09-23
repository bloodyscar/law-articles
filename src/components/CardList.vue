<template>
    <div>
        <div class="card cardlist mt-5" style="overflow:hidden;">
                <div class="wrapper-image" >
                    <img :src=" 'http://127.0.0.1:8000/storage/' + listArticle.thumbnail " class="img-fluid" width="100%" style="object-fit: cover; object-position: center; max-height: 250x;">
                </div>
        </div>
        <div>
            <div class="mt-2">
                <span>Tag: <span class="text-muted mt-3" v-for="item in listArticle.tags" :key="item.id"> #{{ item.name }}</span></span> &nbsp;
                <span class="text-muted" style="margin-top: -15px;" >By {{ listArticle.user.name }} - {{ listArticle.created_at | formatDate }}</span>
                
                
            </div>
            <h5 class="font-weight-bold mt-2">
                <router-link :to=" '/articles/' + listArticle.slug " class="text-dark">
                    {{ listArticle.title }}
                </router-link>
            </h5>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CardList',
    props:['listArticle']
}
</script>

<style scoped>
    div.card{
        border:none;
    }
</style>