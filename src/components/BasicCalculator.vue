<template>
  <div class="calculator">
    <div class="display">
      {{this.current || '0'}}
    </div>
    <div @click="clear()" class="btn">
      {{this.clearState}}
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
      ,
    </div>
    <div @click="equals()" class="btn equals">
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
      opClicked: false,
      clearState: 'AC'
    }
  }, methods: {
    clear() { //CLEAR-METODEN RENSAR BILDRUTAN
      this.current = '0';
      this.logInfo()
    }, sign() { //SIGN-METODEN INVERTERAR TECKNET FÖR DET VISADE VÄRDET
      if (this.current != 0) {
        this.current = this.current.charAt('0') === '-' ?
          this.current.slice(1) : `-${this.current}`;
      }
      this.logInfo()
    }, percent() { //PERCENT-METODEB DIVIDERAR NUVARANSDE VÄRDE MED 100 – 100% = 1, ETC.
      this.current = `${parseFloat(this.current) / 100}`
      this.logInfo()
    }, append(input) { //APEND-METODEN LÄGGER TILL INMATADE VÄRDEN PÅ SLUTET
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
    }, dot() { //DOT-METODEN ANSVARAR FÖR DECIMALTECKNET, TEKNISKT SÄTT ANVÄNDS "," ISTÄLLET FÖR "." PÅ SVENSKA, MEN DET ÄR INTE NÖDVÄNDIGT I M.V.P.
      if (this.current.indexOf(',') === -1) {
        if (this.current !== '0') {
          this.append(',');
        } else {
          this.current = '0,';
        }
        this.logInfo()
      }
    }, setPrevious() {
      this.previous = this.current;
      this.current = '0';
      this.opClicked = true;
      this.clearState = 'C';
    }, devide() { //DIVISION
      this.op = (x, y) => x / y;
      this.setPrevious();
      this.logInfo();
    }, times() { //MULTIPLIKATION
      this.op = (x, y) => x * y;
      this.previous = this.current;
      this.opClicked = true;
      this.setPrevious();
      this.logInfo();
    }, minus() { //SUBTRAKTION
      this.op = (x, y) => x - y;
      this.previous = this.current;
      this.opClicked = true;
      this.setPrevious();
      this.logInfo();
    }, add() { //ADDITION
      this.op = (x, y) => x + y;
      this.previous = this.current;
      this.opClicked = true;
      this.setPrevious();
      this.logInfo();
    }, equals() { //LIKA MED
        this.logInfo();
        console.log('--------------------------------------');
        if (this.previous !== null) {
          this.current = `${Math.round(this.op(parseFloat(this.previous.replaceAll(',', '.')), parseFloat(this.current.replaceAll(',', '.'))) * 1000000000) / 1000000000}`.replaceAll('.', ',') //FLOATING POINT NUMBERS, VÄLDIGT INTRESSANT, SE: YOUTUBE.COM/watch?v=PZRI1IfStY0&ab_channel=Computerphile
          this.previous = null;
        }
        this.clearState = 'AC';
        this.logInfo();
    }, logInfo() { //LOGGAR INFO TILL KONSOLEN
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
  grid-template-columns: 1fr 1fr 1fr 0.75fr;
  grid-auto-rows: minmax(50px, auto);
} .display {
  grid-column: 2 / 5;
  background-color: antiquewhite;
  border: 0.25px solid black;
} .plus {
  grid-row: 5 / 7;
  grid-column: 4 / 5;
} .btn {
  background-color: lightgray;
  border: 0.25px solid black;
} .btn:hover {
  background-color: #C2C2C2;
} .op {
  background-color: orange;
  color: white;
} .op:hover {
  background-color: #EE9400;
} .equals {
  background-color: royalblue;
  color: lightgray;
} .equals:hover {
  background-color: #3058D0;
}
</style>
