<script setup>
import { ref, onMounted } from 'vue'

const emit = defineEmits(['login'])

const mode = ref('login')
const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const message = ref('')
const users = ref([])

onMounted(() => {
  const savedUsers = localStorage.getItem('users')

  if (savedUsers) {
    users.value = JSON.parse(savedUsers)
  } else {
    users.value = [
      {
        email: 'admin@test.com',
        password: 'password123',
      },
    ]

    localStorage.setItem('users', JSON.stringify(users.value))
  }
})

function saveUsers() {
  localStorage.setItem('users', JSON.stringify(users.value))
}

function handleLogin() {
  const foundUser = users.value.find(
    (user) => user.email === email.value && user.password === password.value,
  )

  if (foundUser) {
    message.value = ''
    emit('login')
  } else {
    message.value = 'Invalid email or password.'
  }
}

function createAccount() {
  if (!email.value || !password.value || !confirmPassword.value) {
    message.value = 'Please fill in all fields.'
    return
  }

  if (password.value !== confirmPassword.value) {
    message.value = 'Passwords do not match.'
    return
  }

  const userExists = users.value.some((user) => user.email === email.value)

  if (userExists) {
    message.value = 'This email already has an account.'
    return
  }

  users.value.push({
    email: email.value,
    password: password.value,
  })

  saveUsers()

  message.value = 'Account created. You can now sign in.'
  mode.value = 'login'
  password.value = ''
  confirmPassword.value = ''
}
</script>

<template>
  <main class="login-page">
    <section class="login-card">
      <div class="icon">🎧</div>

      <h1>IT Help Desk</h1>
      <p class="subtitle">Manage support tickets securely</p>

      <div class="tabs">
        <button
          :class="{ active: mode === 'login' }"
          type="button"
          @click="mode = 'login'; message = ''"
        >
          Sign In
        </button>

        <button
          :class="{ active: mode === 'register' }"
          type="button"
          @click="mode = 'register'; message = ''"
        >
          Create Account
        </button>
      </div>

      <form v-if="mode === 'login'" @submit.prevent="handleLogin">
        <input v-model="email" type="email" placeholder="Email address" />

        <input v-model="password" type="password" placeholder="Password" />

        <button class="primary" type="submit">Sign In</button>
      </form>

      <form v-else @submit.prevent="createAccount">
        <input v-model="email" type="email" placeholder="Create email address" />

        <input v-model="password" type="password" placeholder="Create password" />

        <input
          v-model="confirmPassword"
          type="password"
          placeholder="Confirm password"
        />

        <button class="primary" type="submit">Create Account</button>
      </form>

      <p v-if="message" class="message">{{ message }}</p>

      
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
  max-width: 450px;
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
  margin: 0.5rem 0 1.5rem;
  text-align: center;
  color: #9ca3af;
}

.tabs {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
  background-color: #020617;
  padding: 0.4rem;
  border-radius: 12px;
  border: 1px solid #334155;
}

.tabs button {
  border: none;
  padding: 0.75rem;
  border-radius: 9px;
  background: transparent;
  color: #94a3b8;
  cursor: pointer;
  font-weight: bold;
}

.tabs button.active {
  background-color: #2563eb;
  color: white;
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

.primary {
  padding: 0.9rem;
  border: none;
  border-radius: 10px;
  background-color: #2563eb;
  color: white;
  font-weight: bold;
  cursor: pointer;
}

.primary:hover {
  background-color: #1d4ed8;
}

.message {
  margin-top: 1rem;
  color: #facc15;
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