<template>
  <div class="calculator">
    <div class="calculator-screen">
      <calculator-screen
        v-bind:screenText="screenText"
      ></calculator-screen>
    </div>
    <div class="calculator-keyboard">
       <calculator-keyboard
        v-on:number-press="onNumberPress"
        v-on:back-press="removeLastNumber"
        v-on:clear-press="clearInput"
        v-on:plus-press="addNumber"
        v-on:minus-press="subtractNumber"
        v-on:devide-press="devideNumber"
        v-on:multiply-press="multiplyNumber"
        v-on:comma-press="commaNumber"
        v-on:equal-press="getResults"
       ></calculator-keyboard>
    </div>
  </div>
</template>

<script>
import CalculatorScreen from '@/components/CalculatorScreen.vue';
import CalculatorKeyboard from '@/components/CalculatorKeyboard.vue';

export default {
  name: 'Calculator',
  data: function () {
    return {
      screenText: "0"
    }
  },
  methods: {
    onNumberPress: function(number) {
      if(this.screenText.length <= 9){
        if(this.screenText.charAt(0) == "0"){
          this.screenText = this.screenText.substr(1);
        }
        this.screenText += number;
      }
    },
    removeLastNumber: function(){
      this.screenText =  this.screenText.slice(0, -1);
    },
    clearInput: function() {
       this.screenText = "0";
    },
    addNumber: function() {
      if (this.screenText.indexOf('+') > -1) {
        this.getResults("+");
      }

      if(this.screenText.charAt(0) != "0"){
        if(this.screenText.length <= 7 && this.screenText.length >= 1){
          this.screenText = this.screenText + "+";
        }
      }
    },
    subtractNumber: function (){
      if (this.screenText.indexOf('-') > -1) {
        this.getResults("-");
      }

      if(this.screenText.charAt(0) != "0"){
        if(this.screenText.length <= 7 && this.screenText.length >= 1){
          this.screenText = this.screenText + "-";
        }
      }
    },
    multiplyNumber: function (){
      if (this.screenText.indexOf('*') > -1) {
        this.getResults("*");
      }

      if(this.screenText.charAt(0) != "0"){
        if(this.screenText.length <= 7 && this.screenText.length >= 1){
          this.screenText = this.screenText + "*";
        }
      }
    },
    devideNumber: function (){
      if (this.screenText.indexOf('/') > -1) {
        this.getResults("/");
      }

      if(this.screenText.charAt(0) != "0"){
        if(this.screenText.length <= 7 && this.screenText.length >= 1){
          this.screenText = this.screenText + "/";
        }
      }
    },
    commaNumber: function(){
      if(this.screenText.charAt(0) != "0"){
        if(this.screenText.length <= 7 && this.screenText.length >= 1){
          this.screenText = this.screenText + ".";
        }
      }
    },
    getOperations: function(string){
      let addOperator = string.indexOf("+");
      let subOperator = string.indexOf("-");
      let divOperator = string.indexOf("/");
      let multiOperator = string.indexOf("*");

      if(addOperator > 0){
        return "+";
      } else if(subOperator > 0) {
        return "-";
      } else if(divOperator > 0) {
        return "/";
      } else if(multiOperator > 0) {
        return "*";
      }
    },
    getResults: function(delimiter = false){
      if(!delimiter){
        delimiter = this.getOperations(this.screenText);
      }
      let screenText =  this.screenText;
      let text = screenText.split(delimiter);
      let result = 0;

      switch (delimiter) {
        case "+":
          result = Number(text[0]) + Number(text[1]);
          break;
        case "-":
          result = Number(text[0]) - Number(text[1]);
          break;
        case "/":
          result = Number(text[0]) / Number(text[1]);
          break;
         case "*":
          result = Number(text[0]) * Number(text[1]);
          break;
      }

      this.screenText = result.toString();
    }
  },
  components: {
    CalculatorScreen,
    CalculatorKeyboard
  }
}
</script>

<style scoped>
.calculator{
  border: solid 1px #2e7e9c52;
  min-width: 300px;
  display: inline-block;
  background-color: #ebebeb;
  box-shadow: 0 0 10px 1px #5f5f5f7a;
  min-height: 300px;
  padding: 5px;
  box-sizing: border-box;
}
</style>
