<script setup>
defineProps({
  statusFilter: {
    type: String,
    required: true,
  },
})

defineEmits(['update-status-filter'])

const statuses = ['All', 'Open', 'In Progress', 'Closed']
</script>

<template>
  <section class="filter-card">
    <div class="filter-header">
      <span class="filter-icon">⚙️</span>
      <p>Filter by Status</p>
    </div>

    <div class="filter-buttons">
      <button
        v-for="status in statuses"
        :key="status"
        type="button"
        :class="{ active: statusFilter === status }"
        @click="$emit('update-status-filter', status)"
      >
        {{ status }}
      </button>
    </div>
  </section>
</template>

<style scoped>
.filter-card {
  margin-bottom: 1.5rem;
  padding: 1rem;
  background: linear-gradient(145deg, #111827, #0f172a);
  border: 1px solid #263244;
  border-radius: 16px;
  box-shadow: 0 12px 28px rgba(0, 0, 0, 0.25);
}

.filter-header {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #cbd5e1;
  margin-bottom: 0.85rem;
}

.filter-header p {
  margin: 0;
  font-weight: 700;
}

.filter-icon {
  font-size: 1rem;
}

.filter-buttons {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
}

button {
  border: 1px solid #334155;
  padding: 0.7rem 1rem;
  border-radius: 999px;
  background-color: #020617;
  color: #cbd5e1;
  cursor: pointer;
  font-weight: 700;
}

button:hover {
  border-color: #3b82f6;
  color: #ffffff;
}

button.active {
  background-color: #2563eb;
  border-color: #2563eb;
  color: white;
}

@media (max-width: 600px) {
  .filter-buttons {
    flex-direction: column;
  }

  button {
    width: 100%;
  }
}
</style>