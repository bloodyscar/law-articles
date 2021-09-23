<template>
<div>
    <div style=" background-color: #424242;">
        <Navbar />
    </div>
    <div class="container" style="margin-top: 50px;">
        <div class="row">
            <div class="col-md-10">
                <router-link to="/articles"> Back</router-link>
            </div>
            
        </div>
    </div>

    <div class="container" style="margin-top: 50px;">
        <div class="row">
            <div class="col-md-9">
                <CardDetail />
            </div>
            <div class="col-md-3">
                <div class="mt-4">
                    <Sidebar/>
                </div>
            </div>
        </div>
    </div>
    <Footer/>
</div>
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import CardDetail from '@/components/CardDetail.vue'
import Sidebar from '@/components/Sidebar.vue'
import Footer from '@/components/Footer.vue'


export default {
    name:'DetailPage',
    props: ['detail'],
    components:{
        Navbar,
        CardDetail,
        Sidebar,
        Footer
    },
}
</script>

<style>

</style>