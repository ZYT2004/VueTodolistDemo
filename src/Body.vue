<template>
    <div>
        <InputBox/>
        <ul>
            <Tasks/>
        </ul>
        <Funct/>
    </div>
</template>

<script>
import InputBox from './components/InputBox.vue'
import Task from './components/Task.vue'
import Funct from './components/Funct.vue'
export default{
    name:'Body',
    components:{
        InputBox,
        Task,
        Funct
    }
}
</script>

<style scoped>

</style>