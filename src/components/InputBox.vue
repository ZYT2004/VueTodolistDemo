<template>
    <form @submit.prevent>
        <div id='chooseAll' @click='chooseAll' :style="{'visibility':(tasks.length>0 ? 'visible' : 'hidden')}">
            <img :src="(completed ? '/images/cu.png' : '/images/xi.png')" alt='全选'>
        </div>
        <label>
            <input type='text' placeholder='Add your task' v-model='text' name='todo' @keydown.enter='addTask()' autocomplete='off'>
        </label>
    </form>
</template>

<script>
export default{
    name:'InputBox',
    props:{
        tasks:Array
    },
    data(){
        return{
            id:'',
            text:'',
            reminder:false
        }
    },
    computed:{
        completed(){
            let state=1;
            this.tasks.forEach(element => {
                if(element.reminder==false)
                state=0;
            });
            if(state==1)
            return true;
            else return false;
        }
    },
    methods:{
        chooseAll(){
            this.choose=!this.choose;
            if(this.choose==true){
                this.$emit('chooseAll','1');
            }
            else{
                this.$emit('chooseAll','2');
            }
        },
        addTask(){
                if(this.text.trim()!='')
                {
                    const newTask={
                        id:Math.floor(Math.random()*100000),
                        text:this.text.trim(),
                        reminder:false
                    };
                    this.text='';
                    this.$emit('add_Task',newTask);
                }
            }
    },
    emits:['add_Task','chooseAll']
}

</script>

<style scoped>
form{
    background-color:white ;
    display: flex;
    width: 690px;
    height: 65px;
    box-shadow: 0 0px 0px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10);
}
div{
    visibility:hidden;
    display:flex;
    flex-direction:column;
    justify-content:center;
}
img{
    max-width:30px;
    margin:auto 10px;
}
input{
    font-size: 20px;
    outline: none;
    width:635px;
    height:65px;
    border: 0px;
}
input::-webkit-input-placeholder {
    color:#e4cea5;
    font-style: italic;
    font-size: 25px;
}
</style>