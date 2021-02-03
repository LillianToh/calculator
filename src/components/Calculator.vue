<template>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div class="btn" @click="clear()">C</div>
    <div class="btn" @click="sign()">+/-</div>
    <div class="btn" @click="percent()">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div class="btn" @click="append(7)">7</div>
    <div class="btn" @click="append(8)">8</div>
    <div class="btn" @click="append(9)">9</div>
    <div class="btn operator" @click="multiply">x</div>
    <div class="btn" @click="append(4)">4</div>
    <div class="btn" @click="append(5)">5</div>
    <div class="btn" @click="append(6)">6</div>
    <div class="btn operator" @click="minus">-</div>
    <div class="btn" @click="append(1)">1</div>
    <div class="btn" @click="append(2)">2</div>
    <div class="btn" @click="append(3)">3</div>
    <div class="btn operator" @click="add">+</div>
    <div class="zero" @click="append(0)">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
    
</template>

<script>
export default {
  data() {
    return {
      current: "",
      operator: null,
      previous: null,
      operatorClicked: false
    }
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current = this.current.charAt(0) === "-" ? this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current)/100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if(this.current.indexOf(".") === -1) this.append(".");
    },
    divide() {
      this.operator = (a, b) => a/b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    multiply() {
      this.operator = (a, b) => a*b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    minus() {
      this.operator = (a, b) => a-b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    add() {
      this.operator = (a, b) => a+b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    equal() {
      this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`
      this.previous = null;
    }
  }
}
</script>

<style scoped>
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 50px;
  width: 400px;
  margin: 0 auto;
}

.display {
  grid-column: 1 / 5;
  background-color: black;
  color: white;
}

.zero {
  grid-column: 1 / 3;
  border: 1px solid black;
}

.btn {
  border: 1px solid black;
  cursor: pointer;
}

.operator {
  background-color: coral;
  color: white;
}
</style>

