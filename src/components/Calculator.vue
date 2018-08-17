<template>
  <div class="calculator-container">
    <div class="brand-name">Calculator App</div>
    <div class="version">1.0.0-alpha</div>
    <div class="calculator">
      <div class="display">{{ current || '0' }}</div>
      <div @click="clear" class="btn c">C</div>
      <div @click="sign" class="btn">+/-</div>
      <div @click="percent" class="btn">%</div>
      <div @click="divide" class="btn operator">÷</div>
      <div @click="append('7')" class="btn number">7</div>
      <div @click="append('8')" class="btn number">8</div>
      <div @click="append('9')" class="btn number">9</div>
      <div @click="times" class="btn operator">x</div>
      <div @click="append('4')" class="btn number">4</div>
      <div @click="append('5')" class="btn number">5</div>
      <div @click="append('6')" class="btn number">6</div>
      <div @click="subtract" class="btn operator">-</div>
      <div @click="append('1')" class="btn number">1</div>
      <div @click="append('2')" class="btn number">2</div>
      <div @click="append('3')" class="btn number">3</div>
      <div @click="add" class="btn operator">+</div>
      <div @click="append('0')" class="btn zero">0</div>
      <div @click="dot" class="btn">.</div>
      <div @click="equal" class="btn operator equal">=</div>
    </div>
    <div class="name">Kyle Hatch</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
      this.previous = null;
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
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    subtract() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous) 
      )}`;
      this.previous = null;
    }
  }
};
</script>

<style scoped>
.brand-name {
  display: block;
  float: left;
  margin: 0px 0px 10px 5px;
  position: relative;
  color: #ccc;
}

.version {
  display: block;
  float: right;
  margin: 0px 0px 10px 5px;
  position: relative;
  color: #ccc;
}
.name {
  color: #ccc;
}

.calculator {
  margin: 0 auto;
  width: 500px;
  height: 650px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.calculator > div:active:not(.display) {
  filter: brightness(0.75);
}

.display {
  grid-column: 1 / 5;
  background-color: #18ad94;
  color: white;
  padding: 5vmin;
  border-radius: 10px;
  font-family: "Orbitron", sans-serif;
  margin-bottom: 10px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.c {
  background-color: #fa5655 !important;
  color: #fff !important;
}
.zero {
  grid-column: 1 / 3;
}

.number {
  border-radius: 15px;
}
.calculator-container {
  background-color: #32495b;
  padding: 15px;
  width: 510px;
  border-radius: 10px;
  margin: 0 auto;
}
.btn {
  background-color: #fff;
  padding: 1vmin;
  margin: 10px;
  color: #32495b;
  border-radius: 10px;
  font-family: "Orbitron", sans-serif;
}

.btn,
.display {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.operator {
  background-color: #f9b64b;
  color: black;
}
</style>
