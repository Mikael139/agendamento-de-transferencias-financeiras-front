<template>
  <div id="app">
    <div class="container">
      <h1>Sistema de Agendamento de Transferências</h1>

      <div class="card">
        <h2>Agendar Nova Transferência</h2>
        <AgendamentoForm @atualizarExtrato="atualizarExtrato" />
      </div>

      <div class="card">
        <h2>Extrato de Agendamentos</h2>
        <ExtratoList ref="extratoRef" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import AgendamentoForm from "./components/AgendamentoForm.vue";
import ExtratoList from "./components/ExtratoList.vue";

const extratoRef = ref(null);

const atualizarExtrato = () => {
  if (extratoRef.value) {
    extratoRef.value.fetchExtrato();
  }
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f0f2f5;
  margin: 0;
  padding: 0;
}

#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}

.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}

.card {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}
</style>
