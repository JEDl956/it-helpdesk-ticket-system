<script setup>
defineProps({
  tickets: {
    type: Array,
    required: true,
  },
})
</script>

<template>
  <section class="stats">
    <div class="card total">
      <h3>{{ tickets.length }}</h3>
      <p>Total Tickets</p>
    </div>

    <div class="card open">
      <h3>{{ tickets.filter(ticket => ticket.status === 'Open').length }}</h3>
      <p>Open</p>
    </div>

    <div class="card progress">
      <h3>{{ tickets.filter(ticket => ticket.status === 'In Progress').length }}</h3>
      <p>In Progress</p>
    </div>

    <div class="card closed">
      <h3>{{ tickets.filter(ticket => ticket.status === 'Closed').length }}</h3>
      <p>Closed</p>
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
  background-color: #111827;
  border: 1px solid #1f2937;
  padding: 1.5rem;
  text-align: center;
  border-radius: 14px;
  transition: transform 0.2s ease;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
}

.card:hover {
  transform: translateY(-4px);
}

.card h3 {
  margin: 0;
  font-size: 2.4rem;
  font-weight: bold;
}

.card p {
  margin-top: 0.75rem;
  color: #d1d5db;
  font-size: 1rem;
}

.total h3 {
  color: #3b82f6;
}

.open h3 {
  color: #ef4444;
}

.progress h3 {
  color: #f59e0b;
}

.closed h3 {
  color: #22c55e;
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