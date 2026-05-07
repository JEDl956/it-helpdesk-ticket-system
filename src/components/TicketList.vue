<script setup>
import TicketCard from './TicketCard.vue'

defineProps({
  tickets: {
    type: Array,
    required: true,
  },
})

defineEmits(['update-status', 'delete-ticket', 'edit-ticket'])
</script>

<template>
  <section class="ticket-list">
    <div class="list-header">
      <div>
        <h3>Support Tickets</h3>
        <p>{{ tickets.length }} ticket(s) found</p>
      </div>

      <span class="list-icon">📋</span>
    </div>

    <div v-if="tickets.length === 0" class="empty-state">
      <div class="empty-icon">🗂️</div>
      <h4>No tickets found</h4>
      <p>Create a new ticket or change your search/filter options.</p>
    </div>

    <div v-else class="cards">
      <TicketCard
        v-for="ticket in tickets"
        :key="ticket.id"
        :ticket="ticket"
        @update-status="$emit('update-status', ticket.id)"
        @delete-ticket="$emit('delete-ticket', ticket.id)"
        @edit-ticket="$emit('edit-ticket', $event)"
      />
    </div>
  </section>
</template>

<style scoped>
.ticket-list {
  margin-top: 1.5rem;
}

.list-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
  padding: 1rem 1.25rem;
  background: linear-gradient(145deg, #111827, #0f172a);
  border: 1px solid #263244;
  border-radius: 16px;
  color: #f9fafb;
  box-shadow: 0 12px 28px rgba(0, 0, 0, 0.25);
}

.list-header h3 {
  margin: 0;
  font-size: 1.25rem;
}

.list-header p {
  margin: 0.3rem 0 0;
  color: #94a3b8;
  font-size: 0.9rem;
}

.list-icon {
  width: 48px;
  height: 48px;
  display: grid;
  place-items: center;
  background-color: #020617;
  border: 1px solid #334155;
  border-radius: 14px;
  font-size: 1.4rem;
}

.cards {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.empty-state {
  padding: 2rem;
  text-align: center;
  background: linear-gradient(145deg, #111827, #0f172a);
  border: 1px dashed #334155;
  border-radius: 18px;
  color: #f9fafb;
}

.empty-icon {
  font-size: 2rem;
  margin-bottom: 0.75rem;
}

.empty-state h4 {
  margin: 0;
  font-size: 1.2rem;
}

.empty-state p {
  margin: 0.5rem 0 0;
  color: #94a3b8;
}

@media (max-width: 600px) {
  .list-header {
    align-items: flex-start;
  }

  .list-icon {
    display: none;
  }
}
</style>