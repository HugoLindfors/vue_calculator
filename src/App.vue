<script setup>

</script>

<template>
  <div class="calculator">
    <div class="display">
      {{this.current || '0'}}
    </div>
    <div @click="clear()" class="btn">
      C
    </div>
    <div @click="sign()" class="btn">
      +/−
    </div>
    <div @click="percent()" class="btn">
      %
    </div>
    <div @click="devide()" class="btn op">
      ÷
    </div>
    <div @click="append('7')" class="btn">
      7
    </div>
    <div @click="append('8')" class="btn">
      8
    </div>
    <div @click="append('9')" class="btn">
      9
    </div>
    <div @click="times()" class="btn op">
      ×
    </div>
    <div @click="append('4')" class="btn">
      4
    </div>
    <div @click="append('5')" class="btn">
      5
    </div>
    <div @click="append('6')" class="btn">
      6
    </div>
    <div @click="minus()" class="btn op">
      −
    </div>
    <div @click="append('1')" class="btn">
      1
    </div>
    <div @click="append('2')" class="btn">
      2
    </div>
    <div @click="append('3')" class="btn">
      3
    </div>
    <div @click="add()" class="btn plus op">
      +
    </div>
    <div @click="append('0')" class="btn">
      0
    </div>
    <div @click="dot()" class="btn">
      .
    </div>
    <div @click="equals()" class="btn">
      =
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '0',
      op: null,
      opClicked: false
    }
  }, methods: {
    clear() { //CLEAR-METHOD CLEARS THE DISPLAY 
      this.current = '0'
      this.logInfo()
    }, sign() { //SIGN-METHOD INVERTS SIGNAGE FOR THE DISPLAYED VALUE
      if (this.current != 0) {
        this.current = this.current.charAt('0') === '-' ?
          this.current.slice(1) : `-${this.current}`;
      }
      this.logInfo()
    }, percent() { //PERCENT-METHOD DIVIDES CURRENT VALUE WITH 100
      this.current = `${parseFloat(this.current) / 100}`
      this.logInfo()
    }, append(input) { //APEND-METHOD INSERTS IPUT AT THE END OF THE CURRENT DISPLAYED VALUE
      if (this.opClicked) {
        this.current = '';
        this.opClicked = false;
      }
      if (this.current === '0') {
        this.current = input;
      } else {
        this.current = `${this.current}${input}`;
      }
      this.logInfo()
    }, dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
        this.logInfo()
      }
    }, setPrevious() {
      this.previous = this.current;
      this.opClicked = true;
    }, devide() {
      this.op = (x, y) => x / y;
      this.setPrevious();
      this.logInfo();
    }, times() {
      this.op = (x, y) => x * y;
      this.previous = this.current;
      this.opClicked = true;
      this.setPrevious();
      this.logInfo();
    }, minus() {
      this.op = (x, y) => x - y;
      this.previous = this.current;
      this.opClicked = true;
      this.setPrevious();
      this.logInfo();
    }, add() {
      this.op = (x, y) => x + y;
      this.previous = this.current;
      this.opClicked = true;
      this.setPrevious();
      this.logInfo();
    }, equals() {
        this.logInfo();
        console.log('--------------------------------------');
        this.current = `${this.op(parseFloat(this.previous), parseFloat(this.current))}`
        this.previous = null;
        this.logInfo();
    }, logInfo() {
      console.log(`Operator: ${this.op}`);
      console.log(`Previous state: ${this.previous}`);
      console.log(`Current state: ${this.current}`);
      console.log(`Operator clicked: ${this.opClicked}`);
    }
  }
}
</script>

<style scoped>
.calculator {
  height: 100vh;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-auto-rows: minmax(50px, auto);
} .display {
  grid-column: 1 / 5;
  background-color: royalblue;
} .plus {
  grid-row: 5 / 7;
  grid-column: 4 / 5;
} .btn {
  background-color: lightgray;
  border: 0.25px solid black;
} .op {
  background-color: orange;
  color: white;
}
</style>
