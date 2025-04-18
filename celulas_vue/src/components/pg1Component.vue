<script setup>
import { ref } from "vue";

const email = ref("");
const senha = ref("");

function login() {
  alert(`Login com:\nEmail: ${email.value}\nSenha: ${senha.value}`);
}

function registrar() {
  alert("Redirecionando para registro...");
}
</script>

<template>
  <div id="app" class="container">
    <div class="logo-container">
      <h1 class="title">Células</h1>
    </div>
    <h2 class="subtitle">
      Bem vindo <br />
      Faça seu login!
    </h2>
    <div class="form-container">
      <form @submit.prevent="login">
        <div class="input-group">
          <input
            v-model="email"
            class="input"
            placeholder="Email"
            type="email"
            required
          />
        </div>
        <div class="input-group">
          <input
            v-model="senha"
            class="input"
            placeholder="Senha"
            type="password"
            required
          />
        </div>
        <button class="btn-login" type="submit">Login</button>
      </form>
    </div>
    <p class="mt-4">Ainda não tem login?</p>
    <button class="btn-register" @click="registrar">Clique Aqui!</button>
  </div>
</template>

<style scoped>
/* seu CSS aqui */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background-color: #fbbf24; /* bg-yellow-400 */
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100%;
}

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
  font-size: 1.875rem; /* text-3xl */
  font-weight: bold;
  margin-bottom: 1.5rem;
}

.form-container {
  background-color: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 20rem; /* w-80 */
  margin: 0 auto;
}

.input-group {
  margin-bottom: 1rem;
}

.input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #d1d5db; /* border-gray-300 */
  border-radius: 0.375rem; /* rounded-md */
  font-size: 1rem;
  color: #374151; /* text-gray-700 */
}

.input:focus {
  outline: none;
  border-color: #6366f1; /* focus:ring-indigo-500 */
}

.btn-login {
  width: 100%;
  padding: 0.75rem;
  background-color: #000000; /* bg-black */
  color: white;
  font-size: 1rem;
  font-weight: 600;
  border: none;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-login:hover {
  background-color: #1f1f1f; /* Efeito de hover */
}

.btn-register {
  margin-top: 1rem;
  padding: 0.75rem 1.5rem;
  background-color: #000000; /* bg-black */
  color: white;
  font-size: 1rem;
  font-weight: 600;
  border: none;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-register:hover {
  background-color: #1f1f1f; /* Efeito de hover */
}
</style>
