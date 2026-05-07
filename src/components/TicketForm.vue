<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-ticket'])

const title = ref('')
const description = ref('')
const priority = ref('Low')

function submitTicket() {
  if (!title.value || !description.value) {
    alert('Please enter a title and description.')
    return
  }

  emit('add-ticket', {
    title: title.value,
    description: description.value,
    priority: priority.value,
  })

  title.value = ''
  description.value = ''
  priority.value = 'Low'
}
</script>

<template>
  <section class="form-container">
    <h3>Create Ticket</h3>

    <form @submit.prevent="submitTicket">
      <input v-model="title" type="text" placeholder="Ticket Title" />

      <textarea v-model="description" placeholder="Describe the issue"></textarea>

      <select v-model="priority">
        <option>Low</option>
        <option>Medium</option>
        <option>High</option>
      </select>

      <button type="submit">Submit Ticket</button>
    </form>
  </section>
</template>

<style scoped>
.form-container {
  margin-top: 2rem;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

input,
textarea,
select {
  padding: 0.75rem;
}

button {
  background-color: #2563eb;
  color: white;
  border: none;
  padding: 0.75rem;
  cursor: pointer;
}
</style>