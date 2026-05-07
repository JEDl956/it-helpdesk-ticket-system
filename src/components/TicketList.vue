<script setup>
import TicketCard from './TicketCard.vue'

defineProps({
  tickets: {
    type: Array,
    required: true,
  },
})

defineEmits(['update-status', 'delete-ticket'])
</script>

<template>
  <section>
    <h3>Support Tickets</h3>

    <p v-if="tickets.length === 0">No tickets submitted yet.</p>

    <TicketCard
      v-for="ticket in tickets"
      :key="ticket.id"
      :ticket="ticket"
      @update-status="$emit('update-status', ticket.id)"
      @delete-ticket="$emit('delete-ticket', ticket.id)"
    />
  </section>
</template>