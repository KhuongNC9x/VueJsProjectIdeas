<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="calculate('/')">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="calculate('*')">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="calculate('-')">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="calculate('+')">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  name: "CalculatorComponent",
  data() {
    return {
      current: "123",
      calculation: "",
      isCalculate: false,
    };
  },
  methods: {
    clear() {
      this.current = "0";
      this.calculation = "";
      this.isCalculate = false;
    },
    sign() {
      if (this.current === "0") {
        return;
      }

      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    dot() {
      this.current =
        this.current.indexOf(".") > -1
          ? this.current
          : this.current.concat(".");
    },
    append(number) {
      if (this.isCalculate) {
        this.current = number;
      }

      this.current =
        this.current.indexOf(".") > -1 ? this.current.concat(number) : number;

      if (this.current.length > 7) {
        alert("This calculator only supports number with 7 character");
        this.current = this.current.substring(0, 7);
        return;
      }
    },
    equal() {
      this.calculation += this.current;
      this.current = `${Math.round(eval(this.calculation) * 100000) / 100000}`;
      this.calculation = "";
      this.isCalculate = false;
    },
    calculate(operand) {
      this.isCalculate = true;
      this.calculation += this.current + operand;
    },
  },
};
</script>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
}
.btn:hover {
  cursor: pointer;
}
.operator {
  background-color: orange;
  color: white;
}
</style>
