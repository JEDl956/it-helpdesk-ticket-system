<script setup>
defineProps({
  ticket: {
    type: Object,
    required: true,
  },
})

defineEmits(['update-status', 'delete-ticket'])
</script>

<template>
  <article class="ticket-card">
    <h4>{{ ticket.title }}</h4>

    <p>{{ ticket.description }}</p>

    <p><strong>Priority:</strong> {{ ticket.priority }}</p>
    <p><strong>Status:</strong> {{ ticket.status }}</p>
    <p><strong>Created:</strong> {{ ticket.createdAt }}</p>

    <div class="actions">
      <button @click="$emit('update-status')">
        Change Status
      </button>

      <button class="delete" @click="$emit('delete-ticket')">
        Delete
      </button>
    </div>
  </article>
</template>

<style scoped>
.ticket-card {
  border: 1px solid #ccc;
  padding: 1rem;
  margin-top: 1rem;
}

.actions {
  display: flex;
  gap: 0.75rem;
}

button {
  background-color: #2563eb;
  color: white;
  border: none;
  padding: 0.5rem;
  cursor: pointer;
}

.delete {
  background-color: #dc2626;
}
</style>