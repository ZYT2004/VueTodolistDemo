<template>
    <form>
        <div id='chooseAll' @click='chooseAll' :style={'visibility':(tasks.length>0 ? 'visible' : 'hidden')}>
            <img :scr="(completed ? '/public/images/cu.png' : '/public/images/xi.png')" alt='全选'>
        </div>
        <label id='text'>
            <input type='text' placeholder='Add your task' v-model='text' name='todo' @keydown='addTask(e)'>
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
            reminder:false,
            choose:false
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
            if(this.choose==false){
                this.$emit('chooseAll','1');
            }
            else{
                this.$emit('chooseAll','2');
            }
        },
        addTask(e){
            if(e.keyCode==13||e.which==13){
                e.preventDefault();
                if(this.text.trim()!='')
                {
                    const newTask={
                        id:Math.floor(Math.random()*100000),
                        text:this.text.trim(),
                        reminder:false
                    }
                    this.text='';
                    this.$emit('addTask',newTask);
                }
            }
        }
    },
    emits:['addTask','chooseAll']
}

</script>

<style scoped>

</style>