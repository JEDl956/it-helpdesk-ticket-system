<script setup>
import { computed } from 'vue'

const props = defineProps({
  tickets: {
    type: Array,
    required: true,
  },
})

const totalTickets = computed(() => props.tickets.length)
const openTickets = computed(() =>
  props.tickets.filter((ticket) => ticket.status === 'Open').length,
)
const inProgressTickets = computed(() =>
  props.tickets.filter((ticket) => ticket.status === 'In Progress').length,
)
const closedTickets = computed(() =>
  props.tickets.filter((ticket) => ticket.status === 'Closed').length,
)
</script>

<template>
  <section class="stats">
    <div class="card total">
      <div class="icon">🎫</div>
      <div>
        <h3>{{ totalTickets }}</h3>
        <p>Total Tickets</p>
      </div>
    </div>

    <div class="card open">
      <div class="icon">🔴</div>
      <div>
        <h3>{{ openTickets }}</h3>
        <p>Open</p>
      </div>
    </div>

    <div class="card progress">
      <div class="icon">🟡</div>
      <div>
        <h3>{{ inProgressTickets }}</h3>
        <p>In Progress</p>
      </div>
    </div>

    <div class="card closed">
      <div class="icon">🟢</div>
      <div>
        <h3>{{ closedTickets }}</h3>
        <p>Closed</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.25rem;
  margin: 2rem 0;
}

.card {
  display: flex;
  align-items: center;
  gap: 1rem;
  background: linear-gradient(145deg, #111827, #0f172a);
  border: 1px solid #263244;
  padding: 1.4rem;
  border-radius: 18px;
  color: #f9fafb;
  box-shadow: 0 16px 35px rgba(0, 0, 0, 0.3);
  transition: transform 0.2s ease, border-color 0.2s ease;
}

.card:hover {
  transform: translateY(-4px);
  border-color: #3b82f6;
}

.icon {
  width: 52px;
  height: 52px;
  display: grid;
  place-items: center;
  background-color: #020617;
  border: 1px solid #334155;
  border-radius: 14px;
  font-size: 1.4rem;
}

.card h3 {
  margin: 0;
  font-size: 2rem;
  font-weight: 800;
}

.card p {
  margin: 0.25rem 0 0;
  color: #94a3b8;
  font-size: 0.95rem;
}

.total h3 {
  color: #60a5fa;
}

.open h3 {
  color: #f87171;
}

.progress h3 {
  color: #fbbf24;
}

.closed h3 {
  color: #4ade80;
}

@media (max-width: 900px) {
  .stats {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .stats {
    grid-template-columns: 1fr;
  }
}
</style>