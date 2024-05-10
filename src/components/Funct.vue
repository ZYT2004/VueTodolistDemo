<template>
            <div class='function'  :style="{'visibility': (tasks.length>0? 'visible' : 'hidden')}">
                <div><span :textContent='uncomNum'></span><span>items left</span></div>
                <div>
                    <button id="button1" :class="clifir ? 'showBorder' : 'noBorder'" @click="showAll">All</button>
                    <button id="button2" :class="clisec ? 'showBorder' : 'noBorder'" @click="showActive">Active</button>
                    <button id="button3" :class="clithi ? 'showBorder' : 'noBorder'" @click="showCompleted">Completed</button>
                </div>
                <div><button id="button4" @click="$emit('clearTasks')" :style="{'visibility':compExit}">Clear completed</button></div>
            </div>
</template>

<script>
export default{
    name:'Funct',
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
            });
            return num;
        },
        compExit:function(){
            let state=0;
            this.tasks.forEach(element=>{
                if(element.reminder==true){
                    state=1;
                }
            })
            if(state==1){
                return 'visible';
            }else{
                return 'hidden';
            }
        }
    },
    methods:{
        showAll(){
            this.clifir=true;
            this.clisec=false;
            this.clithi=false;
            this.$emit('showSomeType','1');
        },
        showActive(){
            this.clifir=false;
            this.clisec=true;
            this.clithi=false;
            this.$emit('showSomeType','2');
        },
        showCompleted(){
            this.clifir=false;
            this.clisec=false;
            this.clithi=true;
            this.$emit('showSomeType','3');
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
.function{
    width: 690px;
    height: 40px;
    display:flex;
    flex-direction:row;
    justify-content: space-between;
    align-items: center;
    background-color:white;
    box-shadow: 0 5px 5px rgba(0,0,0,0.10),0 0px 0px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10),0 5px 5px rgba(0,0,0,0.10);
}
.function span{
    font-size:15px;
    color:#8993b3;
}
.function span:nth-child(1){
    margin-left: 20px;
}
button{
    text-align: center;
    background-color: white;
    color: #8993b3;
    margin: auto 10px;
    height:25px;
    line-height: 25px;
    padding:0px 10px;
    border:0.5px solid transparent;
}
.noBorder{
    border:0.5px solid transparent;
}
.showBorder{
    border: 0.5px solid #e4cea5;
}
#button4{
    visibility:hidden;
}
</style>