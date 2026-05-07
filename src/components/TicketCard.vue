<script setup>
defineProps({
  ticket: {
    type: Object,
    required: true,
  },
})
</script>

<template>
  <article class="ticket-card">
    <h4>{{ ticket.title }}</h4>

    <p>{{ ticket.description }}</p>

    <p><strong>Priority:</strong> {{ ticket.priority }}</p>
    <p><strong>Status:</strong> {{ ticket.status }}</p>
    <p><strong>Created:</strong> {{ ticket.createdAt }}</p>
  </article>
</template>

<style scoped>
.ticket-card {
  border: 1px solid #ccc;
  padding: 1rem;
  margin-top: 1rem;
}
</style>