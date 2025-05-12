<script setup>
import { ref, onMounted } from 'vue';

// Referências para elementos do DOM
const calendario = ref(null);
const formulario = ref(null);
const diaSelecionado = ref('');
const mesAtualTexto = ref('');

// Dados do calendário
const meses = [
  "Janeiro", "Fevereiro", "Março", "Abril", "Maio", "Junho",
  "Julho", "Agosto", "Setembro", "Outubro", "Novembro", "Dezembro"
];

// Função para abrir o formulário
function abrirFormulario(dia) {
  formulario.value.classList.remove("hidden");
  const hoje = new Date();
  const mes = hoje.getMonth();
  diaSelecionado.value = `Informações para ${dia} de ${meses[mes]}`;
}

// Função para validar o formulário
function validarFormulario(event) {
  event.preventDefault();
  // Implementar validação aqui
  alert('Formulário enviado com sucesso!');
}

// Inicializar o calendário quando o componente for montado
onMounted(() => {
  const hoje = new Date();
  const ano = hoje.getFullYear();
  const mes = hoje.getMonth(); // 0-11
  mesAtualTexto.value = `${meses[mes]} ${ano}`;

  const primeiroDia = new Date(ano, mes, 1).getDay(); // 0-6
  const diasNoMes = new Date(ano, mes + 1, 0).getDate();

  // Adicionar espaços vazios para os dias antes do primeiro dia do mês
  for (let i = 0; i < primeiroDia; i++) {
    const vazio = document.createElement("div");
    calendario.value.appendChild(vazio);
  }

  // Criar botões para cada dia do mês
  for (let dia = 1; dia <= diasNoMes; dia++) {
    const btn = document.createElement("button");
    btn.textContent = dia;
    btn.className = "bg-yellow-100 hover:bg-yellow-300 transition p-3 rounded-lg shadow text-sm";
    btn.onclick = () => abrirFormulario(dia);
    calendario.value.appendChild(btn);
  }
});
</script>

<template>
  <div class="bg-yellow-400 flex flex-col items-center justify-center min-h-screen px-4">
    <h1 class="text-3xl font-bold mb-4">Calendário da Célula</h1>

    <!-- Moldura do Calendário -->
    <div class="bg-white p-6 rounded-xl shadow-lg w-full max-w-2xl">
      <h2 ref="mesAtualTexto" class="text-2xl font-semibold text-center mb-4">{{ mesAtualTexto }}</h2>

      <!-- Grade do calendário -->
      <div class="grid grid-cols-7 gap-2 text-center">
        <div class="font-semibold">Dom</div>
        <div class="font-semibold">Seg</div>
        <div class="font-semibold">Ter</div>
        <div class="font-semibold">Qua</div>
        <div class="font-semibold">Qui</div>
        <div class="font-semibold">Sex</div>
        <div class="font-semibold">Sáb</div>
      </div>
      <div ref="calendario" class="grid grid-cols-7 gap-2 mt-2"></div>
    </div>

    <!-- Formulário -->
    <div
      ref="formulario"
      class="hidden bg-white p-6 mt-6 rounded shadow w-full max-w-md"
    >
      <h2 class="text-xl font-bold mb-4">{{ diaSelecionado }}</h2>
      <form @submit="validarFormulario">
        <label class="block mb-2">Valor Arrecadado:</label>
        <input
          type="text"
          class="w-full p-2 mb-4 border rounded"
          placeholder="Ex: 123,45"
          pattern="^\d+([,]\d{1,2})?$"
          title="Use vírgula como separador decimal (ex: 123,45)"
          required
          id="valor"
        />

        <label class="block mb-2">Quantidade de Pessoas:</label>
        <input
          type="number"
          class="w-full p-2 mb-4 border rounded"
          required
          id="pessoas"
        />

        <label class="block mb-2">Quantidade de Visitantes:</label>
        <input
          type="number"
          class="w-full p-2 mb-4 border rounded"
          required
          id="visitantes"
        />

        <label class="block mb-2">Pessoas Preparadas para Encontro:</label>
        <input
          type="number"
          class="w-full p-2 mb-4 border rounded"
          required
          id="preparadas"
        />

        <button
          type="submit"
          class="bg-black text-white px-4 py-2 rounded w-full"
        >
          Salvar
        </button>
      </form>
    </div>
  </div>
</template>

<style scoped>
/* Estilos adicionais se necessário */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.bg-yellow-400 {
  background-color: #ffb700;
}

.flex {
  display: flex;
}

.flex-col {
  flex-direction: column;
}

.items-center {
  align-items: center;
}

.justify-center {
  justify-content: center;
}

.min-h-screen {
  min-height: 100vh;
}

.px-4 {
  padding-left: 1rem;
  padding-right: 1rem;
}

.text-3xl {
  font-size: 1.875rem;
}

.font-bold {
  font-weight: bold;
}

.mb-4 {
  margin-bottom: 1rem;
}

.bg-white {
  background-color: white;
}

.p-6 {
  padding: 1.5rem;
}

.rounded-xl {
  border-radius: 0.75rem;
}

.shadow-lg {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

.w-full {
  width: 100%;
}

.max-w-2xl {
  max-width: 42rem;
}

.text-2xl {
  font-size: 1.5rem;
}

.font-semibold {
  font-weight: 600;
}

.text-center {
  text-align: center;
}

.grid {
  display: grid;
}

.grid-cols-7 {
  grid-template-columns: repeat(7, minmax(0, 1fr));
}

.gap-2 {
  gap: 0.5rem;
}

.mt-2 {
  margin-top: 0.5rem;
}

.hidden {
  display: none;
}

.mt-6 {
  margin-top: 1.5rem;
}

.rounded {
  border-radius: 0.25rem;
}

.shadow {
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
}

.max-w-md {
  max-width: 28rem;
}

.text-xl {
  font-size: 1.25rem;
}

.block {
  display: block;
}

.mb-2 {
  margin-bottom: 0.5rem;
}

.border {
  border: 1px solid #e5e7eb;
}

.bg-black {
  background-color: #000000;
}

.text-white {
  color: white;
}

.px-4 {
  padding-left: 1rem;
  padding-right: 1rem;
}

.py-2 {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}

/* Manter os estilos originais que não conflitam */
.container {
  text-align: center;
}

.logo-container {
  margin-bottom: 1.5rem;
}

.logo {
  width: 100px;
  height: 100px;
  margin: 0 auto;
}

.title {
  font-size: 2rem;
  font-weight: bold;
  margin-top: 0.5rem;
}

.subtitle {
  font-size: 1.875rem;
  font-weight: bold;
  margin-bottom: 1.5rem;
}

.form-container {
  background-color: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 20rem;
  margin: 0 auto;
}

.input-group {
  margin-bottom: 1rem;
}

.input-group label {
  display: block;
  font-size: 0.875rem;
  font-weight: 500;
  color: #4b5563;
  margin-bottom: 0.25rem;
}

.input-group input,
.input-group select {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #d1d5db;
  border-radius: 0.375rem;
  font-size: 1rem;
  color: #374151;
  transition: border-color 0.3s ease;
}

.input-group input:focus,
.input-group select:focus {
  outline: none;
  border-color: #6366f1;
}

button {
  width: 100%;
  padding: 0.75rem;
  background-color: #000000;
  color: white;
  font-size: 1rem;
  font-weight: 600;
  border: none;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #1f1f1f;
}
</style>