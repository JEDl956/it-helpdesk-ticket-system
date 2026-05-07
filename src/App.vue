<script setup>
import { ref, watch, onMounted, computed } from 'vue'
import Navbar from './components/Navbar.vue'
import DashboardStats from './components/DashboardStats.vue'
import TicketForm from './components/TicketForm.vue'
import TicketList from './components/TicketList.vue'
import SearchBar from './components/SearchBar.vue'

const tickets = ref([])
const search = ref('')

const filteredTickets = computed(() => {
  return tickets.value.filter((ticket) =>
    ticket.title.toLowerCase().includes(search.value.toLowerCase()),
  )
})

onMounted(() => {
  const savedTickets = localStorage.getItem('tickets')

  if (savedTickets) {
    tickets.value = JSON.parse(savedTickets)
  }
})

watch(
  tickets,
  (newTickets) => {
    localStorage.setItem('tickets', JSON.stringify(newTickets))
  },
  { deep: true },
)

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
    <DashboardStats :tickets="tickets" />

    <TicketForm @add-ticket="addTicket" />

    <SearchBar
      :search="search"
      @update-search="search = $event"
    />

    <TicketList
      :tickets="filteredTickets"
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