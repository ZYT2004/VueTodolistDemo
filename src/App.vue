<template>
    <div>
        <Header/>
        <Body/>
        <Footer/>
    </div>
</template>

<script>
import Header from './components/Header.vue'
import Body from './Body.vue'
import Footer from './components/Footer.vue'
export default{
    name:'App',
    components:{
        Header,
        Body,
        Footer
    }
}
</script>

<style scoped>

</style>