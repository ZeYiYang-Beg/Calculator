<script>
export default {
  data() {
    return {
      zero_chance : false,
      previous: null,
      output: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.output = '';
    },
    sign() {
      if (this.output.charAt(0) === '-') {
        this.output.slice(1);
      }
      if (this.output.charAt(0) !== '-' && this.output !== '') {
        this.output = `-${this.output}`;
      }
    },
    percent() {
      this.output = `${parseFloat(this.output / 100)}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.output = '';
        this.operatorClicked = false;
      }
      this.output = `${this.output}${number}`;
    },
    dot() {
      if (this.output.indexOf('.') === -1){
        if (this.output === ''){
          this.append('0');
          this.append('.');
        }
        else {
          this.append('.');
        }
      }
    },
    zero_append() {
      if (this.operatorClicked) {
        this.output = '';
        this.operatorClicked = false;
      }
      if (this.output !== '' || (this.output === '' && this.zero_chance)) {
        this.append('0');
      }
    },
    setPrevious() {
      this.previous = this.output;
      this.operatorClicked = true;
      this.zero_chance = true;
    },
    divide() {
      this.operator = (a,b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a,b) => a * b;
      this.setPrevious();
    },
    sum() {
      this.operator = (a,b) => a + b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a,b) => a - b;
      this.setPrevious();
    },
    equal() {
      this.output = `${this.operator(parseFloat(this.previous), parseFloat(this.output))}`;
      this.previous = null;
    },
  }
}

</script>

<template>
    <div class="container">
      <div class="input">{{ output || '0'}}</div>
      <div class="number-button">
        <div class="number-row">
          <div @click="clear" class="number"><div class="small-number-expect">AC</div></div>
          <div @click="sign" class="number"><div class="small-number-expect">+/-</div></div>
          <div @click="percent" class="number"><div class="small-number-expect">%</div></div>
          <div @click="divide" class="number"><div class="small-number">÷</div></div>
        </div>
        <div class="number-row">
          <div @click="append('7')" class="number"><div class="small-number">7</div></div>
          <div @click="append('8')" class="number"><div class="small-number">8</div></div>
          <div @click="append('9')" class="number"><div  class="small-number">9</div></div>
          <div @click="times" class="number"><div class="small-number">×</div></div>
        </div>
        <div class="number-row">
          <div @click="append('4')" class="number"><div class="small-number">4</div></div>
          <div @click="append('5')" class="number"><div class="small-number">5</div></div>
          <div @click="append('6')" class="number"><div class="small-number">6</div></div>
          <div @click="minus" class="number"><div class="small-number">-</div></div>
        </div>
        <div class="number-row">
          <div @click="append('1')" class="number"><div class="small-number">1</div></div>
          <div @click="append('2')" class="number"><div  class="small-number">2</div></div>
          <div @click="append('3')" class="number"><div  class="small-number">3</div></div>
          <div @click="sum" class="number"><div class="small-number">+</div></div>
        </div>
        <div class="number-row-final">
          <div @click="zero_append" class="number"><div class="small-number">0</div></div>
          <div @click="dot" class="number"><div class="small-number">.</div></div>
          <div @click="equal" class="number"><div class="small-number">=</div></div>
        </div>
      </div>
    </div>
</template>

<style scoped>
  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-content: center;
    background-color: black;
    border-radius: 20px;
    margin: 10px auto;
    border: 1px solid white
  }
  .output {
    display: flex;
    flex-direction: row;
    justify-content: right;
    font-size: 25px;
    border-bottom: 1px solid lightgray;
    padding-right: 15px;
  }
  .input {
    display: flex;
    flex-direction: row;
    justify-content: right;
    font-size: 55px;
    font-weight: bold;
    padding-right: 15px;
  }

  .number-button {
    display: flex;
    flex-direction: column;
    border-top-color: lightgray;
  }

  .number-row {
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }

  .number-row .number:last-child,
  .number-row-final .number:last-child {
    margin-right: 0;
  }

  .number-row:first-child{
    margin-top: 10px;
  }

  .number {
    display: flex;
    width: 135px;
    height: 135px;
    border-radius: 80px;
    background-color: #243b42;
    margin-right: 10px;
    margin-bottom: 5px;
    transition: all 0.5s;
  }

  .number-row-final {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }

  .number-row-final .number {
    margin-bottom: 0;
  }
  .number-row-final .number:first-child {
    flex:2;
  }

  .number-row:first-child .number{
    background-color: lightgray;
  }

  .number:last-child,
  .number-row:first-child .number:last-child{
    background-color: darkorange;
  }

  .number .small-number {
    display: flex;
    justify-items: center;
    align-items: center;
    margin: 0 auto;
    color: white;
    font-size: 50px;
  }

  .number .small-number-expect {
    display: flex;
    justify-items: center;
    align-items: center;
    margin: 0 auto;
    color: black;
    font-size: 50px;
  }


  .number:hover {
    opacity: 0.7;
    cursor: pointer;
  }

</style>
