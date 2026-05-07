<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  ticket: {
    type: Object,
    required: true,
  },
})

const emit = defineEmits(['update-status', 'delete-ticket', 'edit-ticket'])

const isEditing = ref(false)
const editedTitle = ref(props.ticket.title)
const editedDescription = ref(props.ticket.description)

watch(
  () => props.ticket,
  (newTicket) => {
    editedTitle.value = newTicket.title
    editedDescription.value = newTicket.description
  },
  { deep: true },
)

function saveEdit() {
  if (!editedTitle.value.trim() || !editedDescription.value.trim()) {
    return
  }

  emit('edit-ticket', {
    id: props.ticket.id,
    title: editedTitle.value.trim(),
    description: editedDescription.value.trim(),
  })

  isEditing.value = false
}

function cancelEdit() {
  editedTitle.value = props.ticket.title
  editedDescription.value = props.ticket.description
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
    <div class="ticket-top">
      <div class="ticket-info">
        <input
          v-if="isEditing"
          v-model="editedTitle"
          class="edit-input"
          placeholder="Ticket title"
        />

        <h4 v-else class="ticket-title">
          {{ ticket.title }}
        </h4>

        <p class="ticket-id">
          Ticket #{{ ticket.id }}
        </p>
      </div>

      <span class="status-badge" :class="getStatusClass(ticket.status)">
        {{ ticket.status }}
      </span>
    </div>

    <textarea
      v-if="isEditing"
      v-model="editedDescription"
      class="edit-textarea"
      placeholder="Ticket description"
    ></textarea>

    <p v-else class="description">
      {{ ticket.description }}
    </p>

    <div class="details">
      <div>
        <span class="label">Priority</span>
        <span class="priority" :class="getPriorityClass(ticket.priority)">
          {{ ticket.priority }}
        </span>
      </div>

      <div>
        <span class="label">Created</span>
        <span>{{ ticket.createdAt }}</span>
      </div>
    </div>

    <div class="actions">
      <button class="btn status" @click="$emit('update-status')">
        Change Status
      </button>

      <button v-if="!isEditing" class="btn edit" @click="isEditing = true">
        Edit
      </button>

      <template v-else>
        <button class="btn save" @click="saveEdit">
          Save
        </button>

        <button class="btn cancel" @click="cancelEdit">
          Cancel
        </button>
      </template>

      <button class="btn delete" @click="$emit('delete-ticket')">
        Delete
      </button>
    </div>
  </article>
</template>

<style scoped>
.ticket-card {
  background: linear-gradient(145deg, #111827, #0f172a);
  border: 1px solid #263244;
  border-radius: 18px;
  padding: 1.5rem;
  margin-top: 1rem;
  color: #f9fafb;
  box-shadow: 0 16px 35px rgba(0, 0, 0, 0.35);
}

.ticket-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 1rem;
}

.ticket-info {
  flex: 1;
}

.ticket-title {
  margin: 0;
  font-size: 1.15rem;
  color: #ffffff;
}

.ticket-id {
  margin: 0.35rem 0 0;
  font-size: 0.85rem;
  color: #94a3b8;
}

.description {
  margin: 1rem 0;
  line-height: 1.6;
  color: #cbd5e1;
}

.details {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin: 1rem 0;
}

.details div {
  min-width: 150px;
  padding: 0.8rem;
  background-color: #020617;
  border: 1px solid #263244;
  border-radius: 12px;
}

.label {
  display: block;
  margin-bottom: 0.3rem;
  color: #94a3b8;
  font-size: 0.8rem;
}

.priority {
  font-weight: bold;
}

.actions {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
  margin-top: 1rem;
}

.edit-input,
.edit-textarea {
  width: 100%;
  padding: 0.85rem;
  background-color: #020617;
  color: #f9fafb;
  border: 1px solid #334155;
  border-radius: 10px;
}

.edit-textarea {
  min-height: 100px;
  margin-top: 1rem;
  resize: vertical;
}

.btn {
  border: none;
  padding: 0.7rem 1rem;
  cursor: pointer;
  border-radius: 10px;
  color: white;
  font-weight: 700;
}

.status,
.edit,
.save {
  background-color: #2563eb;
}

.status:hover,
.edit:hover,
.save:hover {
  background-color: #1d4ed8;
}

.cancel {
  background-color: #64748b;
}

.cancel:hover {
  background-color: #475569;
}

.delete {
  background-color: #dc2626;
}

.delete:hover {
  background-color: #b91c1c;
}

.status-badge {
  padding: 0.45rem 0.8rem;
  border-radius: 999px;
  color: white;
  font-size: 0.8rem;
  font-weight: 700;
  white-space: nowrap;
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
  color: #f87171;
}

.medium {
  color: #fbbf24;
}

.low {
  color: #4ade80;
}

@media (max-width: 600px) {
  .ticket-top {
    flex-direction: column;
  }

  .actions {
    flex-direction: column;
  }

  .btn {
    width: 100%;
  }
}
</style>