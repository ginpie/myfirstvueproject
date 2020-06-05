<template>
  <div>
  <h1>Calculator</h1>
  <div class="calculator">
    <div class="display"> {{current || 0}} </div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "-1000",
      operator: null,
      previous: null,
      operatorClicked: false,
    }
  },

  methods: {
    clear(){
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(num) {
      if (this.operatorClicked){
        this.current='';
        this.operatorClicked = false;
      }
      if (parseFloat(this.current) != 0.0){
        this.current = `${this.current}${num}`;
      } else {this.current = '0';}
    },
    dot(){
      if (this.current.indexOf('.') === -1){
        this.append('.');
      }
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    add(){
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    minus(){
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    equal(){
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous))}`;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .calculator {
    font-size: 30px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    width: 300px;
    margin: 0 auto;
  }
  .display {
    grid-column: 1 / 5;
    height: 50px;
    background-color: #333;
    color: white;
  }
  .zero {
    grid-column: 1 / 3;
  }

  .btn {
    border: 1px solid #999;
    background-color: #f2f2f2;
  }

  .operator {
    background-color: orange;
    color: white;
  }
</style>
