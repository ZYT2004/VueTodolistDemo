<template>
    <div>
        <InputBox :tasks='tasks' @add_Task='addTask' @chooseAll='chooseAll'/>
        <ul v-for='task in tasks' :key='task.id' >
            <Task :task='task' :status='status' @chooseTask='chooseTask' @deleteTask='deleteTask'/>
        </ul>
        <Funct :tasks='tasks' :status='status' @clearTasks='clearTasks' @showSomeType='showSomeType'/>
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
    },
    data(){
        return{
            tasks:Array,
            status:String
        }
    },
    methods:{
        addTask(newTask){
            this.tasks.push(newTask);
            console.log(newTask);
        },
        chooseAll(state){
            if(state=='1'){
                this.tasks.forEach((task) => {
                    task.reminder=true;
                });
            }
            if(state=='2'){
                this.tasks.forEach((task)=>{
                    task.reminder=false;
                })
            }
        },
        chooseTask(id){
            this.tasks=this.tasks.map((task)=>{
                if(task.id==id){
                    task.reminder=!task.reminder;
                    return task;
                }
                return task;
            })
        },
        deleteTask(id){
            console.log(id);
            this.tasks=this.tasks.filter((task)=>task.id!==id)
        },
        clearTasks(){
            this.tasks=this.tasks.filter((task)=>task.reminder==false)
        },
        showSomeType(index){
            this.status=index;
        }
    },
    created(){
        if(window.localStorage.getItem('tasks')){
            this.tasks=JSON.parse(window.localStorage.getItem('tasks'));
        }else{
            this.tasks=[];
        }
        if(window.localStorage.getItem('status')){
            this.status=window.localStorage.getItem('status');
        }else{
            this.status='1';
        }
    },
    watch:{
        tasks:{
            handler(newValue){
                window.localStorage.setItem('tasks',JSON.stringify(newValue));
            },
            deep:true
        },
        status:{
            handler(newValue){
                window.localStorage.setItem('status',newValue);
            }
        }
    }
}
</script>

<style scoped>
div {
    display:flex;
    flex-direction:column;
    justify-items: flex-start;
    align-items: center;
    background-color: #d3e9d7;
}
*{
    margin:0px;
    padding:0px;
}
ul{
    display:flex;
    flex-direction: column;
    align-items: center;
}
</style>