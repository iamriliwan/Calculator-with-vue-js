<template>
  <div class="calculator">
    <h5>Riliwan Calculator</h5>
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="division" class="btn operator">/</div>
    <div @click="append ('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiplication" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtraction" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="equal" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClick: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClick){
        this.current = '';
        this.operatorClick = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.operatorClick = true;
      this.previous = this.current;
    },
    addition() {
      this.operator = (a, b) => a + b;
    },
    subtraction() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    multiplication() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    division() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    equal() {
      this.current =  `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  margin: 0 auto;
  width: 40%;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);

}
.display {
  grid-column: 1/5;
  background-color: green;
  color: white;
  font-size: 35px;

}
.zero {
  grid-column: 1/3;
  cursor: pointer !important;
}
.btn :hover{
  cursor: pointer !important;
}
.btn {
  background-color: black;
  color: white;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: bold;
  border: 1px solid white;
  cursor: pointer !important;
}
.operator {
  background-color: white;
  color: red;
  border: 1px solid black;
  cursor: pointer !important;
}
</style>
