<template>
<div>
    <div class="card" style="overflow:hidden;">
        <div class="wrapper-image" style="max-height:250px;">
            <img :src=" 'https://apilawarticlez.herokuapp.com/' + article.thumbnail " class="img-fluid" width="100%" style="object-fit: cover; object-position: center;">
        </div>
    </div>
    <div>
        <p class="mt-2">Tag: <span class="text-muted" v-for="item in article.tags" :key="item.id">#{{ item.name}}&nbsp;</span></p>
        <p class="text-muted mt-2" style="margin-top: -15px;">By Adit Hernowo • 23 Juli, 2021</p>
        <h5 class="font-weight-bold"  style="margin-top: -5px;"><router-link :to=" '/articles/' + article.slug" class=" text-dark">
            {{ article.title  }}
        </router-link></h5>
        
    </div>
</div>
</template>

<script>
export default {
    name:'Card',
    props:['article']
}
</script>

<style>

</style>