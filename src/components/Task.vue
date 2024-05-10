<template>
    <li class="showarea" :style="{'display' : showSomeType}" @mouseover="ifshow=true" @mouseout="ifshow=false">
        <div class='choose' @click="chooseTask">
            <img :src="task.reminder ? '/images/xuanzhong.png' : '/images/weixuanzhong.png'" alt='是否选中'>
        </div>
        <input v-model='task2.text' @blur="check" :class="(task.reminder ? 'completed' : 'notComp')" readonly ondblclick="this.readonly=false" onchange="this.readonly=true">
        <div class='delete' @mouseover="ifcu=true" @mouseout="ifcu=false" @click="deleteTask" :style="{'visibility' : (ifshow ? 'visible' : 'hidden')}">
            <img :src="(ifcu ? '/images/cushanchu.png' : '/images/xishanchu.png')" alt='是否删除'>
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
            task2:this.task,
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
            return style;
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
            this.$emit('deleteTask',this.task.id);
        }
    },
    emits:['chooseTask','deleteTask']
}
</script>

<style scoped>
li{
    background-color:white ;
    display: flex;
    width: 690px;
    height: 65px;
    box-shadow: 0 0px 0px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10);
}
.notComp {
    transition:all 0.5s;
    font-size: 25px;
    outline: none;
    width:690px;
    height:65px;
    border: 0px;
    text-decoration: none;
    color: black;
}
.completed{
    transition:all 0.5s;
    font-size: 25px;
    outline: none;
    width:690px;
    height:65px;
    border: 0px;
    text-decoration: line-through;
    color:#e4cea5;
}
.choose{
    display:flex;
    flex-direction:column;
    justify-content:center;
}
.delete{
    visibility:hidden;
    display:flex;
    flex-direction:column;
    justify-content:center;
}
.choose img{
    max-width:30px;
    margin:auto 20px;
}
.delete img{
    max-width:30px;
    margin:auto 20px;
}
</style>