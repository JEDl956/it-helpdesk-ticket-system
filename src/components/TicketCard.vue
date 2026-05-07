<script setup>
import { ref } from 'vue'

const props = defineProps({
  ticket: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits([
  'update-status',
  'delete-ticket',
  'edit-ticket',
])

const isEditing = ref(false)

const editedTitle = ref(props.ticket.title)
const editedDescription = ref(props.ticket.description)

function saveEdit() {
  emit('edit-ticket', {
    id: props.ticket.id,
    title: editedTitle.value,
    description: editedDescription.value,
  })

  isEditing.value = false
}

function getStatusClass(status) {
  if (status === 'Open') return 'open'
  if (status === 'In Progress') return 'progress'
  return 'closed'
}

function getPriorityClass(priority) {
  if (priority === 'High') return 'high'
  if (priority === 'Medium') return 'medium'
  return 'low'
}
</script>

<template>
  <article class="ticket-card">
    <div class="header">
      <template v-if="isEditing">
        <input v-model="editedTitle" />
      </template>

      <template v-else>
        <h4>{{ ticket.title }}</h4>
      </template>

      <span :class="getStatusClass(ticket.status)">
        {{ ticket.status }}
      </span>
    </div>

    <template v-if="isEditing">
      <textarea v-model="editedDescription"></textarea>
    </template>

    <template v-else>
      <p class="description">
        {{ ticket.description }}
      </p>
    </template>

    <div class="details">
      <p>
        <strong>Priority:</strong>

        <span :class="getPriorityClass(ticket.priority)">
          {{ ticket.priority }}
        </span>
      </p>

      <p>
        <strong>Created:</strong>
        {{ ticket.createdAt }}
      </p>
    </div>

    <div class="actions">
      <button @click="$emit('update-status')">
        Change Status
      </button>

      <button v-if="!isEditing" @click="isEditing = true">
        Edit
      </button>

      <button v-else @click="saveEdit">
        Save
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
  flex-wrap: wrap;
}

input,
textarea {
  width: 100%;
  padding: 0.6rem;
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

.high {
  color: #dc2626;
  font-weight: bold;
}

.medium {
  color: #f59e0b;
  font-weight: bold;
}

.low {
  color: #16a34a;
  font-weight: bold;
}
</style>