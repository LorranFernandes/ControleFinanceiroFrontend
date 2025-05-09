<template>
  <div class="tabela-container">
    <h2>Contas Cadastradas</h2>
    <button @click="carregar">🔄 Recarregar</button>
    <table>
      <thead>
        <tr>
          <th>Nome</th>
          <th>Valor</th>
          <th>Tipo</th>
          <th>Categoria</th>
          <th>Vencimento</th>
          <th>Parcelas</th>
          <th>Recorrência</th>
          <th>Pago</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="conta in contas" :key="conta.id">
          <td>{{ conta.nome }}</td>
          <td>{{ conta.valor }}</td>
          <td>{{ conta.tipo }}</td>
          <td>{{ conta.categoria }}</td>
          <td>{{ conta.data_vencimento }}</td>
          <td>{{ conta.parcelas ?? '-' }}</td>
          <td>{{ conta.recorrencia_meses ?? '-' }}</td>
          <td>
            <input type="checkbox" :checked="conta.esta_paga" @change="atualizarStatus(conta)" />
          </td>
          <td>
            <button @click="excluir(conta.id)">🗑</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import api from '../services/api'

const contas = ref<any[]>([])

async function carregar() {
  try {
    const res = await api.get('/contas')
    contas.value = res.data
  } catch (error) {
    alert('Erro ao carregar contas')
  }
}

async function excluir(id: number) {
  await api.delete(`/contas/${id}`)
  await carregar()
}

async function atualizarStatus(conta: any) {
  await api.patch(`/contas/${conta.id}/pagar`, { esta_paga: !conta.esta_paga })
  await carregar()
}

onMounted(() => {
  carregar()
})
</script>

<style scoped>
.tabela-container {
  max-width: 1000px;
  margin: 20px auto;
}
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  border: 1px solid #ccc;
  padding: 8px;
  text-align: center;
}
button {
  cursor: pointer;
}
</style>
