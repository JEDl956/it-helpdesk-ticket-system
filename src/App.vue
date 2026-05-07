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

function updateStatus(id) {
  const ticket = tickets.value.find((ticket) => ticket.id === id)

  if (ticket.status === 'Open') {
    ticket.status = 'In Progress'
  } else if (ticket.status === 'In Progress') {
    ticket.status = 'Closed'
  } else {
    ticket.status = 'Open'
  }
}

function deleteTicket(id) {
  tickets.value = tickets.value.filter((ticket) => ticket.id !== id)
}
</script>

<template>
  <Navbar />

  <main class="container">
    <TicketForm @add-ticket="addTicket" />

    <TicketList
      :tickets="tickets"
      @update-status="updateStatus"
      @delete-ticket="deleteTicket"
    />
  </main>
</template>

<style scoped>
.container {
  padding: 2rem;
  font-family: Arial, sans-serif;
}
</style>