<template>
  <form @submit.prevent="agendar">
    <div class="form-group">
      <label for="contaOrigem">Conta de Origem</label>
      <input id="contaOrigem" v-model="form.contaOrigem" placeholder="Ex: XXXXXXXXXX" required />
    </div>
    <div class="form-group">
      <label for="contaDestino">Conta de Destino</label>
      <input id="contaDestino" v-model="form.contaDestino" placeholder="Ex: XXXXXXXXXX" required />
    </div>
    <div class="form-group">
      <label for="valor">Valor (R$)</label>
      <input id="valor" type="number" v-model.number="form.valor" placeholder="Ex: 1000.00" step="0.01" required />
    </div>
    <div class="form-group">
      <label for="dataTransferencia">Data da Transferência</label>
      <input id="dataTransferencia" type="date" v-model="form.dataTransferencia" required />
    </div>

    <button type="submit">Agendar</button>

    <p v-if="successMessage" class="message success">{{ successMessage }}</p>
    <p v-if="errorMessage" class="message error">{{ errorMessage }}</p>
  </form>
</template>

<script>
import axios from 'axios';
import { ref } from 'vue';

export default {
  setup() {
    const form = ref({
      contaOrigem: '',
      contaDestino: '',
      valor: 0,
      dataTransferencia: '',
      dataAgendamento: new Date().toISOString().slice(0, 10),
    });

    const successMessage = ref('');
    const errorMessage = ref('');

    const agendar = async () => {
      successMessage.value = '';
      errorMessage.value = '';

      try {
        const response = await axios.post('http://localhost:8080/api/transferencias/agendar', form.value);
        successMessage.value = `Transferência agendada com sucesso! ID: ${response.data.id}`;
      } catch (error) {
        if (error.response) {
          errorMessage.value = 'Transferência não permitida! Não há taxa aplicável para a data de transferência fornecida. ' + error.response.data;
        } else {
          errorMessage.value = 'Erro de rede: ' + error.message;
        }
      }
    };

    return { form, agendar, successMessage, errorMessage };
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}
.form-group {
  text-align: left;
}
label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}
input {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  border-radius: 4px;
  border: 1px solid #ddd;
}
button {
  padding: 10px 15px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #3aa870;
}
.message {
  padding: 10px;
  border-radius: 4px;
  font-weight: bold;
  margin-top: 10px;
}
.success {
  color: green;
  background-color: #e6f7e6;
}
.error {
  color: red;
  background-color: #fde6e6;
}
</style>