<script setup>
import { ref } from 'vue'

const emit = defineEmits(['login'])

const email = ref('')
const password = ref('')
const error = ref('')

function handleLogin() {
  if (email.value === 'admin@test.com' && password.value === 'password123') {
    emit('login')
    error.value = ''
  } else {
    error.value = 'Invalid email or password.'
  }
}
</script>

<template>
  <section class="login-card">
    <h2>IT Help Desk Login</h2>

    <form @submit.prevent="handleLogin">
      <input v-model="email" type="email" placeholder="Email" />

      <input v-model="password" type="password" placeholder="Password" />

      <button type="submit">Login</button>

      <p v-if="error" class="error">{{ error }}</p>
    </form>

    <p class="hint">Test Login: admin@test.com / password123</p>
  </section>
</template>

<style scoped>
.login-card {
  max-width: 400px;
  margin: 5rem auto;
  background-color: white;
  padding: 2rem;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

input {
  padding: 0.75rem;
}

button {
  background-color: #2563eb;
  color: white;
  border: none;
  padding: 0.75rem;
  cursor: pointer;
}

.error {
  color: #dc2626;
  text-align: center;
}

.hint {
  margin-top: 1rem;
  font-size: 0.9rem;
  text-align: center;
}
</style>