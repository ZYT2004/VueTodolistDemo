<template>
    <ul>
        <li>
            <div>
                <div><span :textContent='uncomNum'></span><span>items left</span></div>
                <div>
                    <button id="button1" :class="clifir ? 'showBorder' : 'noBorder'" @click="showAll">All</button>
                    <button id="button2" :class="clisec ? 'showBorder' : 'noBorder'" @click="showActive">Active</button>
                    <button id="button3" :class="clithi ? 'showBorder' : 'noBorder'" @click="showCompleted">Completed</button>
                </div>
                <div><button id="button4" @click="$emit('clearTasks')" :style="{'visibility':comExist}">Clear completed</button></div>
            </div>
        </li>
        <li></li>
        <li></li>
    </ul>
</template>

<script>
export default{
    name:'Body',
    data(){
        return{
            clifir:Boolean,
            clisec:Boolean,
            clithi:Boolean
        }
    },
    props:{
        tasks:Array,
        status:String
    },
    computed:{
        uncomNum:function(){
            let num=0;
            this.tasks.forEach(element=>{
                if(element.reminder==false){
                    num++;
                }
            })
            return num;
        },
        comExist:function(){
            let state=0;
            this.tasks.forEach(element=>{
                if(element.reminder==true){
                    state=1;
                }
            })
            if(state==0){
                return 'hidden';
            }else{
                return 'visible';
            }
        }
    },
    methods:{
        showAll(){
            this.clifir=true;
            this.clisec=false;
            this.clithi=false;
            $emit('showSomeType','1');
        },
        showActive(){
            this.clifir=false;
            this.clisec=true;
            this.clithi=false;
            $emit('showSomeType','2');
        },
        showCompleted(){
            this.clifir=false;
            this.clisec=false;
            this.clithi=true;
            $emit('showSomeType','3');
        }
    },
    created(){
        switch(this.status){
            case '1':{
                this.clifir=true;
                this.clisec=false;
                this.clithi=false;
                break;
            }
            case '2':{
                this.clifir=false;
                this.clisec=true;
                this.clithi=false;
                break;
            }
            case '3':{
                this.clifir=false;
                this.clisec=false;
                this.clithi=true;
                break;
            }
        }
    },
    emits:['clearTasks','showSomeType']
}
</script>

<style scoped>

</style>