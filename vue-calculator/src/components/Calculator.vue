<template >
  <div class="calculator">
      <div class="buttons-grid" >
            <div class="display"> {{displayValue}} </div>
            <div class="buttons" @click="updateOutput(button)" v-for="button in buttons" :key="button.text" :class="button.class">
                <div >{{button.text}}</div>
            </div>
      </div>
  </div>
</template>

<script>
export default {
    name:'calculator',
    data(){
        return{
            title:'Vue-Calculator',
            displayValue: '0',
            operand1: null,
            operator: null,
            waitingForSecondOperand: false,
            buttons:[
                {text:7,class:'operand'},
                {text:8,class:'operand'},
                {text:9,class:'operand'},
                {text:'%',class:'operator'},
                {text:4,class:'operand'},
                {text:5,class:'operand'},
                {text:6,class:'operand'},
                {text:'X',class:'operator'},
                {text:1,class:'operand'},
                {text:2,class:'operand'},
                {text:3,class:'operand'},
                {text:'-',class:'operator'},
                {text:'AC',class:'operator'},
                {text:0,class:'operand'},
                {text:'=',class:'operator'},
                {text:'+',class:'operator'},
                ],
        }
    },
    methods:{
        calculate: function(operand1, operand2, operator){
              switch (operator){
                case "+":
                return operand1 + operand2;
                case "-":
                return operand1 - operand2;
                case "%":
                return operand1 / operand2;
                case "X":
                return operand1 * operand2;
                default:
                return Infinity;
              }
        },
        updateOutput: function(button){

            if(button.class== 'operand'){
                if(this.waitingForSecondOperand === true){
                    this.displayValue = button.text;
                    this.waitingForSecondOperand = false;
                }else{
                    this.displayValue = this.displayValue === '0' ? button.text : this.displayValue +""+button.text;
                }
            }
            else{
                if(button.text == 'AC'){                
                    this.displayValue = '0';
                    this.operand1 = null;
                    this.waitingForSecondOperand = false;
                    this.operator = null;
                }else{
                    if(this.operator != null && this.waitingForSecondOperand){
                        this.operator = button.text;
                        return;                       
                    }
                    if(this.operand1 == null){
                        this.operand1 = parseInt(this.displayValue);
                    }else if(this.operator != null){
                        var result = this.calculate(this.operand1,parseInt(this.displayValue),this.operator);
                        this.displayValue = result;
                        this.operand1 = result;
                    }
                    this.waitingForSecondOperand = true;
                    this.operator = button.text;
                }                                                                   
            }
        }    
    }
}
</script>

<style scoped>

.calculator{
    width:50%;
    margin: auto;
    height: 500px;
}
.display{
    grid-column: 1/5;
    border-radius: 15px 15px 0px 0px;
    background-color: #fcd861;
    height: 50%;
    text-align: right;
    padding: 0.5em;
    font-weight: bolder;
    font-size: 1.5em ;
    color:#ff5733;
    width:90%;
    margin: auto;
    border: 0.5px solid pink;
}
 .buttons-grid{
    text-align: center;
    padding: 20px;
    font-weight: bold;
    font-size: 1.5em ;
    color:white;
    border:1px solid #f0ac9c;
    box-shadow: 7px 5px  #f7866da1;
    border-radius: 0px 0px 15px 15px;
    background-color:rgb(4, 204, 204);
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    width:40%;
    margin: auto;
    height: 500px;
    margin-top: 5px;
}
.buttons{
    border: 1px solid #fcd861;
    margin: 5%;
    padding-top: 25%;
    /* padding-top:15%; */
}
div .buttons.operator{
    padding: auto;
    background-color: #ff0048 ;
}
div .buttons.operand{
    background-color: #ff5733;
}
div .buttons.operator:hover{
    background-color: #c70039;
    color:white;
    border: 3px solid #ffc400;
}
div .buttons.operand:hover{
    background-color: #ff2f00;
    color:white;
     border: 3px solid #ffc400;
}
div .buttons.buttons.operand:active{
    background-color: cyan;
}
div .buttons.operator:active{
    background-color: cyan;
}
</style>
