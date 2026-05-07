<script setup>
import { ref } from 'vue'
import Navbar from './components/Navbar.vue'
import TicketForm from './components/TicketForm.vue'
import TicketList from './components/TicketList.vue'

const tickets = ref([])

function addTicket(ticket) {
  tickets.value.push({
    id: Date.now(),
    ...ticket,
    status: 'Open',
    createdAt: new Date().toLocaleDateString(),
  })
}
</script>

<template>
  <Navbar />

  <main class="container">
    <TicketForm @add-ticket="addTicket" />

    <TicketList :tickets="tickets" />
  </main>
</template>

<style scoped>
.container {
  padding: 2rem;
  font-family: Arial, sans-serif;
}
</style>