<script setup>

import { reactive } from 'vue';

const estado = reactive({
  num1: 0,
  num2: 0,
  result: 0,
  selectOption: "adicao"
});

const operador = reactive({
  adicaoSinal: "+",
  subtracaoSinal: "-",
  multiplicacaoSinal: "x",
  divisaoSinal: "/"
});

const soma = () => {
  return estado.num1 + estado.num2;
}

const subtrai = () => {
  return estado.num1 - estado.num2;
}

const multiplica = () => {
  return estado.num1 * estado.num2;
}

const divide = () => {
  return estado.num1 / estado.num2;
}

const getOperador = () => {
  switch(estado.selectOption) {
    case "adicao": 
      return operador.adicaoSinal;
    case "subtracao": 
      return operador.subtracaoSinal;
    case "multiplicacao": 
      return operador.multiplicacaoSinal;
    case "divisao": 
      return operador.divisaoSinal;
    default:
      return operador.adicaoSinal;
  }
}

const calculo = () => {
  const { selectOption } = estado;

  switch(selectOption) {
    case "adicao":
      estado.result = soma();
      break;
    case "subtracao":
      estado.result = subtrai();
      break;
    case "multiplicacao":
      estado.result = multiplica();
      break;
    case "divisao":
      estado.result = divide();
      break;
    default:
      estado.result = 0;
  }
}

</script>

<template>
  
<header>
  <div class = "container p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>Calculadora aritmética</h1>
    <p>Coloque dois números nos campos vazios para receber o resultado</p>
  </div>
</header>
<main>
  <div class = "container">
    <form>
      <div class = "row align-items-center">
        <div class = "col-md-3">
          <input @keyup = "calculo" v-model = "estado.num1" type = "number" class = "form-control" required>
        </div>
        <div class = "col-md-1 text-center">
          <span>{{ getOperador() }}</span>
        </div>
        <div class = "col-md-3">
          <input @keyup = "calculo" v-model = "estado.num2" type = "number" class = "form-control" required>
        </div> 
        <div class = "col-md-1 text-center">
          <span>=</span>
        </div>
        <div class = "col-md-2">
          <span>{{ estado.result }}</span>
        </div> 
        <div class = "col-md-2">
          <select @change = "calculo" v-model = "estado.selectOption" class = "form-control">
            <option value="adicao">Adição</option>
            <option value="subtracao">Subtração</option>
            <option value="multiplicacao">Multiplicação</option>
            <option value="divisao">Divisão</option>
          </select>
        </div> 
      </div>
    </form>
  </div>
</main>

</template>

<style scoped>
</style>
