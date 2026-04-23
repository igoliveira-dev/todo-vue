<script setup>
import { reactive } from 'vue'

const nome = "igu"
const meuObj = {
  nome: "Igor",
  time: "Santos"
}

function dizOla() {
  return `${nome} diz oi`
}

const batman = "https://www.correiobraziliense.com.br/cbradar/wp-content/uploads/2026/03/Gemini_Generated_Image_7p0igt7p0igt7p0i-2-1.png"
const superman = "https://static.wikia.nocookie.net/dccomics/images/0/08/Summer_of_Superman_Special_Vol_1_1_Textless.jpg/revision/latest?cb=20250725150153&path-prefix=pt"

const gostaDoBatman = true
const gostaDoSuperman = false

// let contador = 0

const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['igor', 'gian', 'paulo', 'monica'],
  nomeAInserir: ''
})

function incrementar() {
  estado.contador++;
}

function decrementar() {
  estado.contador--;
}

function atualizaSaldo() {
  const { saldo, transferindo } = estado
  return saldo - transferindo
}

function validaTransferencia() {
  const { saldo, transferindo } = estado
  return saldo >= transferindo
}

function cadastraNome() {
  estado.nomes.push(estado.nomeAInserir)
}

</script>

<template>
  <h1>{{ dizOla() }}</h1>
  <img v-if="gostaDoBatman" :src="batman" alt="">
  <img v-else-if="gostaDoSuperman" :src="superman" alt="">
  <h2  v-else>Não gosta de heróis</h2>

  <br />
  <hr />

  {{ estado.contador }}
  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br />
  <hr />

  {{ estado.email }}
  <input type="email" @keyup="evento => estado.email = evento.target.value">

  <br />
  <hr />

  Saldo: {{ estado.saldo }} <br>
  Transferindo: {{ estado.transferindo }} <br>
  Saldo depois da transferência: {{ atualizaSaldo() }}  <br>
  <input :class="{ invalido: !validaTransferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">

  <br>
  <hr>

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>
  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
  <button type="button" @click="cadastraNome()">Cadastrar nome</button>

</template>

<style scoped>

img {
  max-width: 200px;
}

.invalido {
  outline-color: red;
  border-color: red;
}

</style>
