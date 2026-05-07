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
  <main class="login-page">
    <section class="login-card">
      <div class="icon">🎧</div>

      <h1>IT Help Desk</h1>
      <p class="subtitle">Sign in to manage support tickets</p>

      <form @submit.prevent="handleLogin">
        <input v-model="email" type="email" placeholder="Email address" />

        <input v-model="password" type="password" placeholder="Password" />

        <button type="submit">Sign In</button>

        <p v-if="error" class="error">{{ error }}</p>
      </form>

      <div class="test-box">
        <p><strong>Test Account</strong></p>
        <p>admin@test.com / password123</p>
      </div>
    </section>
  </main>
</template>

<style scoped>
.login-page {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  background:
    radial-gradient(circle at top left, rgba(37, 99, 235, 0.35), transparent 35%),
    radial-gradient(circle at bottom right, rgba(14, 165, 233, 0.2), transparent 35%),
    #0f172a;
}

.login-card {
  width: 100%;
  max-width: 430px;
  background-color: #111827;
  border: 1px solid #1f2937;
  padding: 2.5rem;
  border-radius: 18px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.45);
}

.icon {
  width: 60px;
  height: 60px;
  margin: 0 auto 1rem;
  display: grid;
  place-items: center;
  background-color: #2563eb;
  border-radius: 16px;
  font-size: 1.8rem;
}

h1 {
  margin: 0;
  color: #f9fafb;
  text-align: center;
}

.subtitle {
  margin: 0.5rem 0 2rem;
  text-align: center;
  color: #9ca3af;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

input {
  padding: 0.9rem;
  background-color: #020617;
  color: white;
  border: 1px solid #334155;
  border-radius: 10px;
}

button {
  padding: 0.9rem;
  border: none;
  border-radius: 10px;
  background-color: #2563eb;
  color: white;
  font-weight: bold;
  cursor: pointer;
}

button:hover {
  background-color: #1d4ed8;
}

.error {
  color: #f87171;
  text-align: center;
}

.test-box {
  margin-top: 1.5rem;
  padding: 1rem;
  background-color: #020617;
  border: 1px solid #334155;
  border-radius: 10px;
  color: #cbd5e1;
  text-align: center;
  font-size: 0.9rem;
}

.test-box p {
  margin: 0.25rem 0;
}
</style>