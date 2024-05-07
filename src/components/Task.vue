<template>
    <li class="showarea" id="task.id" :style='{'display' : showSomeType}' @mouseover="ifshow=true" @mouseout="ifshow=false">
        <div class='choose' @click="chooseTask">
            <img :src="(task.reminder ? '/public/images/xuanzhong.png' : '/public/images/weixuanzhong.png')" alt='是否选中'>
        </div>
        <input v-model='this.task.text' @blur="check":class="(singleTask.reminder ? 'completed' : 'notComp')" readonly ondblclick="this.readonly=false" onchange="this.readonly=true">
        <div class='delete' @mouseover="ifcu=true" @mouseout="ifcu=false" @click="deleteTask" :style="{'visibility' : (ifshow ? 'visible' : 'hidden')}">
            <img :src="(ifcu ? '/public/images/cushanchu.png' : '/public/images/xishanchu.png')" alt='是否删除'>
        </div>
    </li>
</template>

<script>
export default{
    name:'Task',
    props:{
        task:Object,
        status:String
    },
    data(){
        return{
            ifcu:false,
            ifshow:false
        }
    },
    computed:{
        showSomeType(){
            let style;
            switch(this.status){
                case '1':{
                    style='flex';
                    break;
                }
                case '2':{
                    if(this.task.reminder==false){
                        style='flex';
                    }else{
                        style='none';
                    }
                    break;
                }
                case '3':{
                    if(this.task.reminder==true){
                        style='flex';
                    }else{
                        style='none';
                    }
                    break;
                }
            }
        }
    },
    methods:{
        chooseTask(){
            this.$emit('chooseTask',this.task.id);
        },
        check(){
            if(this.task.text=='')
            this.$emit('deleteTask',this.task.id);
        },
        deleteTask(){
            this.$emit('deleteTask',this.task,id);
        }
    },
    emits:['chooseTask','deleteTask']
}
</script>

<style scoped>

</style>