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
    <div class="card">
      <h3>{{ tickets.length }}</h3>
      <p>Total Tickets</p>
    </div>

    <div class="card">
      <h3>{{ tickets.filter(ticket => ticket.status === 'Open').length }}</h3>
      <p>Open</p>
    </div>

    <div class="card">
      <h3>{{ tickets.filter(ticket => ticket.status === 'In Progress').length }}</h3>
      <p>In Progress</p>
    </div>

    <div class="card">
      <h3>{{ tickets.filter(ticket => ticket.status === 'Closed').length }}</h3>
      <p>Closed</p>
    </div>
  </section>
</template>

<style scoped>
.stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
  margin: 2rem 0;
}

.card {
  border: 1px solid #ddd;
  padding: 1rem;
  text-align: center;
  border-radius: 8px;
  background-color: #f9fafb;
}

.card h3 {
  margin: 0;
  color: #2563eb;
  font-size: 2rem;
}

.card p {
  margin: 0.5rem 0 0;
}
</style>