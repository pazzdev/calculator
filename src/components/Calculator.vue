<template>
  <div id="calcWrapper">
      <Display v-bind:currentValue=currentValue v-bind:displayValue=displayValue></Display>
      <div class="calc-btn-block">
        <div class="calc-box scientific-box">
            <Button   v-for="sb in scientificButtons" 
                        v-bind:key="sb.id" 
                        v-bind:buttonOption="sb"
                        v-on:handle-press="handlePress">
            </Button>
        </div>
        <div class="calc-box math-box">
            <Button   v-for="mb in mathButtons" 
                        v-bind:key="mb.id" 
                        v-bind:buttonOption="mb"
                        v-on:handle-press="handlePress" >
            </Button>
        </div>
      </div>      
  </div>
</template>

<script>
import Display from './Display.vue'
import Button from './Button.vue'

export default {
  data: function () {
      return {
          currentValue:"0",
          lastValue:"0",
          displayValue:"",
          currentAnswer:"",
          previousOperation:"",          
         
          scientificButtons:[
              {
                  id: 21,
                  name: "Rad  |  Deg",
                  isOther: false,
                  isOperator: true,
                  isRd: true
              },
              {
                  id: 22,
                  name: "x!",
                  isOther: false,
                  isOperator: true
              },
              {
                  id: 23,
                  name: "Inv",
                  isOther: false,
                  isOperator: true
              },
              {
                  id: 24,
                  name: "sin",
                  isOther: false,
                  isOperator: true
              },
              {
                  id: 25,
                  name: "In",
                  isOther: false,
                  isOperator: true
              },
              {
                  id: 26,
                  name: "π",
                  isOther: false,
                  isOperator: true
              },
              {
                  id: 27,
                  name: "cos",
                  isOther: false,
                  isOperator: true
              },
              {
                  id: 28,
                  name: "log",
                  isOther:false,
                  isOperator: true
              },
              {
                  id: 29,
                  name: "e",
                  isOther:false,
                  isOperator: true
              },
              {
                  id: 30,
                  name: "tan",
                  isOther:false,
                  isOperator: true
              },
              {
                  id: 31,
                  name: "√",
                  isOther:false,
                  isOperator: true              
                },
              {
                  id: 32,
                  name: "Ans",
                  isOther:false,
                  isOperator: true
              },
              {
                  id: 33,
                  name: "EXP",
                  isOther:false,
                  isOperator: true
              },
              {
                  id: 34,
                  name: "xy",
                  isOther:false,
                  isOperator: true
              }
          ],
          mathButtons:[
              {
                  id: 1,
                  name: "(",
                  isOther: false,
                  isOperator:true
              },
              {
                  id: 2,
                  name: ")",
                  isOther: false,
                  isOperator:true
              },
              {
                  id: 3,
                  name: "%",
                  isOther: false,
                  isOperator:true              
                },
              {
                  id: 4,
                  name: "CE",
                  isOther: false,
                  isOperator:true
              },
              {
                  id: 5,
                  name: "7",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 6,
                  name: "8",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 7,
                  name: "9",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 8,
                  name: "÷",
                  isOther: false,
                  isOperator: true,
                  isMathSymbol:true
              },
              {
                  id: 9,
                  name: "4",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 10,
                  name: "5",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 11,
                  name: "6",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 12,
                  name: "x",
                  isOther: false,
                  isOperator: true,
                  isMathSymbol:true
              },
              {
                  id: 13,
                  name: "1",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 14,
                  name: "2",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 15,
                  name: "3",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 16,
                  name: "−",
                  isOther: false,
                  isOperator: true,
                  isMathSymbol:true
              },
              {
                  id: 17,
                  name: "0",
                  isOther: true,
                  isOperator: false
              },
              {
                  id: 18,
                  name: ".",
                  isOther: true,
                  isOperator: false,
                  isMathSymbol:true
              },
              {
                  id: 19,
                  name: "=",
                  isOther: false,
                  isOperator: false,
                  isEqual: true,
                  isMathSymbol:true
              },
              {
                  id: 20,
                  name: "+",
                  isOther: false,
                  isOperator: true,
                  isMathSymbol:true
              }
          ]
      }
  },
  components:{
      Display,
      Button
  },
  methods: {
      handlePress: function (event){
          var number = event.textContent.trim();
          switch (number){
              case "CE": this.clearDisplay();
                break;
              case "0":
              case "1":
              case "2":
              case "3":
              case "4":
              case "5":
              case "6":
              case "7":
              case "8":
              case "9": this.numberPressed(number);
              break;
              case "+": (this.previousOperation !== 'operator') ? this.operatorPressed("+") : '';
                break;
              case "x": (this.previousOperation !== 'operator') ? this.operatorPressed("x") : '';
                break;
              case "=": (this.previousOperation !== 'operator') ? this.equalPressed() : '';
                break;
              case ".": (this.previousOperation !== 'operator') ? this.addDecimalPoint() : '';
                  break;
              default:
                  alert("Currently, this key is not working.");
          }
      },
      addDecimalPoint: function() {
        if (this.lastValue.indexOf(".") < 0){
            this.currentValue += "."
            this.lastValue += "."
        }
      },
      numberPressed: function(number){
          this.previousOperation = 'number';
          if (this.currentValue === "0"){
              this.currentValue = number;
              this.lastValue = number;
          }
          else {  
            this.currentValue += number;
            this.lastValue += number;            
          }          
      },
      
      operatorPressed: function (operator){
        this.previousOperation = 'operator';          
        this.currentValue = this.currentValue + " " + operator + " "
        this.lastValue = '';
        if(this.currentAnswer !== ''){
            this.displayValue = "Ans = " + this.currentAnswer
        }
      },
      equalPressed: function(){
        if(this.currentValue !== "0" && this.previousOperation !== 'equal'){
            let currentValueArray = this.currentValue.split(' ');
            currentValueArray = (currentValueArray.map((el) => isNaN(el) ? (el === 'x' ? '*' : el) : parseFloat(el))).join('')                 
            this.displayValue = this.currentValue + " =  "
            this.currentValue = ""+eval(`${currentValueArray}`)
            this.currentAnswer = this.currentValue;
            this.lastValue = this.currentValue;
            this.previousOperation = 'equal';
            if (this.currentValue.length >= 50){
                throw "DISPLAY ERROR: Result will not fit on display.";
            }
        }
      },
      clearDisplay: function (){
          this.currentValue = "0";
          this.lastValue = "0";
          if(this.currentAnswer !== ''){
            this.displayValue = "Ans = " + this.currentAnswer
          }
      }
  }
}
</script>