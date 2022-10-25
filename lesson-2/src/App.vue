<template>
  <div id="app">
    <input v-on:click="activateOperand(1)" type="number" v-model="operand1" />
    <input v-on:click="activateOperand(2)" type="number" v-model="operand2" />

    <p>Результат: {{ result }} </p>

    <div v-show="error" class="error"> {{ error }} </div>


    <!-- операторы     -->
    <button v-for="item, index of operations" v-bind:key="index" v-on:click="currentOperation = item">{{ item
    }}</button>

    <!-- кнопка меняющая операнд -->
    <p>Операнд {{ activeOperand }}</p>

    <!-- чекбокс, которым можно скрывать и показывать блок с экранной клавиатурой -->
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{{ displayKeyboard }}</label>

    <!-- клавиатура -->
    <div v-show="checked">
      <button v-for="item, index of keyboard" v-bind:key="index" v-on:click="currentNumber = item">{{ item }}</button>
    </div>


    <!-- история  -->
    <ul>
      <li v-for="item, index of logList" v-bind:key="index">{{ item }}</li>
    </ul>

  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      displayKeyboard: 'Отобразить экранную клавиатуру',
      checked: '',
      keyboard: [
        '0',
        '1',
        '2',
        '3',
        '4',
        '5',
        '6',
        '7',
        '8',
        '9',
        '←',
      ],
      currentNumber: '0',
      activeOperand: 1,
      operand1: 0,
      operand2: 0,
      currentOperation: '+',
      error: '',
      operations: [  // список доступных операций
        '+',
        '-',
        '*',
        '/'
      ],
      logList: {},
      lastKey: 0
    }
  },
  computed: {     // вычисляемые свойства
    result() {
      return this.doCalc(this.currentOperation)
    }
  },
  methods: {
    activateOperand(id) {
      this.activeOperand = id;
    },
    sum() {
      return Number(this.operand1) + Number(this.operand2)
    },
    subtraction() {
      return this.operand1 - this.operand2
    },
    multiplication() {
      return this.operand1 * this.operand2
    },
    division() {
      if (Number(this.operand2) == 0) {
        this.error = 'На ноль делить нельзя'
        return
      }
      return this.operand1 / this.operand2
    },
    doCalc(operator) {
      this.error = '';

      this.$set(this.logList, String(this.lastKey++), `${new Date().toDateString()}: ${this.operand1} ${operator} ${this.operand2}`)

      switch (operator) {
        case "+":
          return this.sum()
        case "-":
          return this.subtraction()
        case "*":
          return this.multiplication()
        case "/":
          return this.division()
        default:
          break;
      }
    },
    writeNumber(number) {
      switch (number) {
        case "0":
          return this.operand1 + Number('0');
        case "1":
          return this.operand1 + '1';
        case "2":
          return this.multiplication()
        case "3":
          return this.division()
        default:
          break;
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.error {
  color: darkred;
  border: 1px solid darkred;
  padding: 10px 20px;
  display: block;
  margin: 20px 0;
}
</style>
