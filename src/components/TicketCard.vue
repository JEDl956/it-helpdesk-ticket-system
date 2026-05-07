<script setup>
defineProps({
  ticket: {
    type: Object,
    required: true,
  },
})

defineEmits(['update-status', 'delete-ticket'])

function getStatusClass(status) {
  if (status === 'Open') return 'open'
  if (status === 'In Progress') return 'progress'
  return 'closed'
}
</script>

<template>
  <article class="ticket-card">
    <div class="header">
      <h4>{{ ticket.title }}</h4>

      <span :class="getStatusClass(ticket.status)">
        {{ ticket.status }}
      </span>
    </div>

    <p class="description">
      {{ ticket.description }}
    </p>

    <div class="details">
      <p><strong>Priority:</strong> {{ ticket.priority }}</p>
      <p><strong>Created:</strong> {{ ticket.createdAt }}</p>
    </div>

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
  background-color: white;
  border-radius: 10px;
  padding: 1.25rem;
  margin-top: 1rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.description {
  margin: 1rem 0;
}

.details {
  margin-bottom: 1rem;
}

.actions {
  display: flex;
  gap: 1rem;
}

button {
  border: none;
  padding: 0.6rem 1rem;
  cursor: pointer;
  border-radius: 6px;
  background-color: #2563eb;
  color: white;
}

.delete {
  background-color: #dc2626;
}

.open,
.progress,
.closed {
  padding: 0.4rem 0.75rem;
  border-radius: 20px;
  color: white;
  font-size: 0.85rem;
}

.open {
  background-color: #dc2626;
}

.progress {
  background-color: #f59e0b;
}

.closed {
  background-color: #16a34a;
}
</style>