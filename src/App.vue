<template>
    <div class='father'>
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
.father{
    display:flex;
    flex-direction:column;
    justify-items: flex-start;
    align-items: center;
    background-color:#d3e9d7;
    height:100vh;
}
</style>