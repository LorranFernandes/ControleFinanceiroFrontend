<template>
  <form @submit.prevent="enviarConta" class="formulario">
    <h2>Lançar nova conta</h2>

    <label>Nome:</label>
    <input v-model="conta.nome" placeholder="Nome da conta" />

    <label>Valor:</label>
    <input v-model.number="conta.valor" placeholder="Valor" type="number" />

    <label>Tipo:</label>
    <select v-model="conta.tipo">
      <option disabled value="">Selecione o tipo</option>
      <option value="cheque">Cheque</option>
      <option value="periodica">Periódica</option>
      <option value="parcelada">Parcelada</option>
    </select>

    <label>Categoria:</label>
    <input v-model="conta.categoria" placeholder="Categoria" />

    <label>Data de vencimento:</label>
    <input v-model="conta.data_vencimento" type="date" />

    <!-- Parcelas -->
    <template v-if="conta.tipo === 'parcelada'">
        <label>Parcelas:</label>
        <input v-model.number="conta.parcelas" type="number" placeholder="Número de parcelas" />
    </template>

    <!-- Recorrência -->
    <template v-if="conta.tipo === 'periodica'">
        <label>Meses recorrentes:</label>
        <input v-model.number="conta.recorrencia_meses" type="number" placeholder="Meses de repetição" />
    </template>

    <!-- Campos extras para cheque -->
    <template v-if="conta.tipo === 'cheque'">
        <label>Número da Conta:</label>
        <input v-model="conta.numero_conta" placeholder="Número da Conta" />

        <label>Banco:</label>
        <input v-model="conta.banco" placeholder="Banco" />

        <label>Titular:</label>
        <input v-model="conta.titular" placeholder="Titular" />

        <label>Beneficiário:</label>
        <input v-model="conta.beneficiario" placeholder="Beneficiário" />
    </template>

    <button type="submit">Salvar</button>
  </form>
</template>

<script setup lang="ts">
import { reactive } from 'vue'
import api from '../services/api'

const conta = reactive({
  nome: '',
  tipo: '',
  valor: 0,
  categoria: '',
  data_vencimento: '',
  parcelas: null,
  recorrencia_meses: null,
  esta_paga: false,
  numero_conta: '',
  banco: '',
  titular: '',
  beneficiario: ''
})

async function enviarConta() {
  try {
    console.log(JSON.stringify(conta, null, 2))
    await api.post('/contas', conta)
    alert('Conta cadastrada!')
    Object.assign(conta, {
      nome: '',
      tipo: '',
      valor: 0,
      categoria: '',
      data_vencimento: '',
      parcelas: null,
      recorrencia_meses: null,
      esta_paga: false
    })
  } catch (error) {
    alert('Erro ao cadastrar')
  }
}
</script>

<style scoped>
.formulario {
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-width: 400px;
  margin: 0 auto;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
}
input, select {
  padding: 8px;
  font-size: 1em;
}
button {
  margin-top: 10px;
  padding: 10px;
  background: green;
  color: white;
  border: none;
  cursor: pointer;
}


</style>
