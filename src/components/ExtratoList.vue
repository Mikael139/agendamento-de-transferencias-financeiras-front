<template>
  <div>
    <p v-if="loading">Carregando extrato...</p>
    <p v-else-if="extrato.length === 0">Nenhum agendamento encontrado.</p>
    <table v-else class="extrato-table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Conta de Origem</th>
          <th>Conta de Destino</th>
          <th>Valor</th>
          <th>Taxa</th>
          <th>Data Agendamento</th>
          <th>Data Transferência</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="transferencia in extrato" :key="transferencia.id">
          <td>{{ transferencia.id }}</td>
          <td>{{ transferencia.contaOrigem }}</td>
          <td>{{ transferencia.contaDestino }}</td>
          <td>R$ {{ transferencia.valor.toFixed(2) }}</td>
          <td>R$ {{ transferencia.taxa.toFixed(2) }}</td>
          <td>{{ formatarData(transferencia.dataAgendamento) }}</td>
          <td>{{ formatarData(transferencia.dataTransferencia) }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted, defineExpose } from "vue";
import axios from "axios";

const extrato = ref([]);
const loading = ref(true);

const fetchExtrato = async () => {
  loading.value = true;
  try {
    const response = await axios.get("http://localhost:8080/api/transferencias/extrato");
    extrato.value = response.data;
  } catch (error) {
    console.error("Erro ao buscar o extrato:", error);
  } finally {
    loading.value = false;
  }
};

const formatarData = (data) => {
  if (!data) return "";
  const [ano, mes, dia] = data.split("-");
  return `${dia}/${mes}/${ano}`;
};

defineExpose({ fetchExtrato });

onMounted(fetchExtrato);
</script>

<style scoped>
.extrato-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
.extrato-table th,
.extrato-table td {
  border: 1px solid #ddd;
  padding: 12px;
  text-align: left;
}
.extrato-table th {
  background-color: #f2f2f2;
  font-weight: bold;
}
</style>
