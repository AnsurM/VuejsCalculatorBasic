<template>
  <div id="app">
    <label for='num1'>Number 1:</label>
    <input id='num1' type="number" v-model='number1' v-on:keyup.enter='onPressEnter'/>
    <label for='num2'>Number 2:</label>
    <input id='num2' type="number" v-model='number2' v-on:keyup.enter='onPressEnter'/>
    <br />
    <div>
      <br />
        <button id='add' v-on:click='onClickOperation'>+</button>
        <button id='sub' v-on:click='onClickOperation'>-</button>
        <button id='mul' v-on:click='onClickOperation'>*</button>
        <button id='divide' v-on:click='onClickOperation'>/</button>
      <br />
    </div>
      <br />
    <p id='nullWarn'>{{this.warning}}</p>
    <p id='resultText'>Result is: {{this.result}}</p>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    let number1 = null;
    let number2 = null;
    let result = null;
    let warning = '';
    return {
      number1,
      number2,
      result,
      warning
    }
  },

  methods: {
    onPressEnter(event) {
      console.log(event.target.id);
      if(event.target.id === 'num1')
      console.log("Number 1: ", this.number1);
      else {
        console.log("Number 2: ", this.number2);
      }
    },
    onClickOperation(event) {
      console.log("Operation requested: ", event.target.id);
      let answer = 0;

      if(this.number1 === null || this.number2 === null)
      {
        console.log("One of the numbers is missing!");
        this.warning = "One of the numbers is missing!";
        return;
      }

      let operand1 = (this.number1.includes('.') ? parseFloat(this.number1) : parseInt(this.number1));
      let operand2 = (this.number2.includes('.') ? parseFloat(this.number2) : parseInt(this.number2));
      switch(event.target.id) {
          case ('add'): 
          {
            answer = operand1 + operand2;
            break;
          }
          case ('sub'): 
          {
            answer = operand1 - operand2;
            break;
          }
          case ('mul'): 
          {
            answer = operand1 * operand2;
            break;
          }
          case ('divide'): 
          {
            answer = (operand1 / operand2);
            console.log(answer.toString().length);
            answer = answer.toString().length > 3 ? answer.toFixed(3) : answer;
            break;
          }
          default: answer = null; break;
      }
        console.log(answer);
          this.result = (typeof answer !== null) ? answer : null;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
