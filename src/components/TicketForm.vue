<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-ticket'])

const title = ref('')
const description = ref('')
const priority = ref('Low')
const message = ref('')

function submitTicket() {
  if (!title.value.trim() || !description.value.trim()) {
    message.value = 'Please enter a title and description.'
    return
  }

  emit('add-ticket', {
    title: title.value.trim(),
    description: description.value.trim(),
    priority: priority.value,
  })

  title.value = ''
  description.value = ''
  priority.value = 'Low'
  message.value = 'Ticket created successfully.'
}
</script>

<template>
  <section class="form-container">
    <div class="form-header">
      <div>
        <h3>Create New Ticket</h3>
        <p>Submit a support request for the IT team.</p>
      </div>

      <span class="form-icon">🛠️</span>
    </div>

    <form @submit.prevent="submitTicket">
      <div class="field">
        <label>Ticket Title</label>
        <input v-model="title" type="text" placeholder="Example: Printer is not working" />
      </div>

      <div class="field">
        <label>Description</label>
        <textarea
          v-model="description"
          placeholder="Describe the issue with details"
        ></textarea>
      </div>

      <div class="field">
        <label>Priority</label>
        <select v-model="priority">
          <option>Low</option>
          <option>Medium</option>
          <option>High</option>
        </select>
      </div>

      <button type="submit">Submit Ticket</button>

      <p v-if="message" class="message">{{ message }}</p>
    </form>
  </section>
</template>

<style scoped>
.form-container {
  margin-top: 2rem;
  padding: 1.5rem;
  background: linear-gradient(145deg, #111827, #0f172a);
  border: 1px solid #263244;
  border-radius: 18px;
  color: #f9fafb;
  box-shadow: 0 16px 35px rgba(0, 0, 0, 0.3);
}

.form-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.form-header h3 {
  margin: 0;
  font-size: 1.4rem;
}

.form-header p {
  margin: 0.35rem 0 0;
  color: #94a3b8;
}

.form-icon {
  width: 52px;
  height: 52px;
  display: grid;
  place-items: center;
  background-color: #020617;
  border: 1px solid #334155;
  border-radius: 14px;
  font-size: 1.5rem;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 0.45rem;
}

label {
  color: #cbd5e1;
  font-size: 0.9rem;
  font-weight: 700;
}

input,
textarea,
select {
  width: 100%;
  padding: 0.9rem;
  background-color: #020617;
  color: #f9fafb;
  border: 1px solid #334155;
  border-radius: 10px;
  outline: none;
}

textarea {
  min-height: 110px;
  resize: vertical;
}

input:focus,
textarea:focus,
select:focus {
  border-color: #3b82f6;
}

button {
  margin-top: 0.5rem;
  background-color: #2563eb;
  color: white;
  border: none;
  padding: 0.9rem;
  cursor: pointer;
  border-radius: 10px;
  font-weight: 800;
}

button:hover {
  background-color: #1d4ed8;
}

.message {
  margin: 0;
  text-align: center;
  color: #4ade80;
  font-weight: 700;
}

@media (max-width: 600px) {
  .form-header {
    align-items: flex-start;
  }

  .form-icon {
    display: none;
  }
}
</style>