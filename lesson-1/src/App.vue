<template>
  <div>
    <div class="display">
      <input type="number" v-model="operand1" /> <!-- v-model связывает тег с переменной из скрипта -->
      <input type="number" v-model="operand2" />
    </div>

    <p>Результат: {{ result }}</p>

    <div class="keyboard">
      <button v-on:click="result = Number(operand1) + Number(operand2)">+</button>
      <button v-on:click="result = Number(operand1) - Number(operand2)">-</button>
      <button v-on:click="result = Number(operand1) * Number(operand2)">*</button>
      <button v-on:click="result = Number(operand1) / Number(operand2)">/</button>
      <button v-on:click="result = Math.pow(operand1, operand2)">^</button>
      <button v-on:click="result = Math.trunc(Number(operand1) / Number(operand2))">integer division</button>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      operand1: 0,
      operand2: 0,
      result: 0
    }
  }
}
</script>

<style lang="scss">

</style>
