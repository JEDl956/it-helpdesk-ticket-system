<script setup>
import { ref, watch, onMounted, computed } from 'vue'
import Navbar from './components/Navbar.vue'
import DashboardStats from './components/DashboardStats.vue'
import TicketForm from './components/TicketForm.vue'
import TicketList from './components/TicketList.vue'
import SearchBar from './components/SearchBar.vue'
import StatusFilter from './components/StatusFilter.vue'
import LoginForm from './components/LoginForm.vue'

const isLoggedIn = ref(false)
const tickets = ref([])
const search = ref('')
const statusFilter = ref('All')

const filteredTickets = computed(() => {
  return tickets.value.filter((ticket) => {
    const searchText = search.value.toLowerCase()

    const matchesSearch =
      ticket.title.toLowerCase().includes(searchText) ||
      ticket.description.toLowerCase().includes(searchText) ||
      ticket.priority.toLowerCase().includes(searchText)

    const matchesStatus =
      statusFilter.value === 'All' || ticket.status === statusFilter.value

    return matchesSearch && matchesStatus
  })
})

onMounted(() => {
  const savedTickets = localStorage.getItem('tickets')
  const savedLogin = localStorage.getItem('isLoggedIn')

  if (savedTickets) {
    tickets.value = JSON.parse(savedTickets)
  }

  if (savedLogin === 'true') {
    isLoggedIn.value = true
  }
})

watch(
  tickets,
  (newTickets) => {
    localStorage.setItem('tickets', JSON.stringify(newTickets))
  },
  { deep: true },
)

watch(isLoggedIn, (value) => {
  localStorage.setItem('isLoggedIn', value)
})

function login() {
  isLoggedIn.value = true
}

function logout() {
  isLoggedIn.value = false
}

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

  if (!ticket) return

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

function editTicket(updatedTicket) {
  const ticket = tickets.value.find((ticket) => ticket.id === updatedTicket.id)

  if (ticket) {
    ticket.title = updatedTicket.title
    ticket.description = updatedTicket.description
  }
}
</script>

<template>
  <LoginForm v-if="!isLoggedIn" @login="login" />

  <template v-else>
    <Navbar :total-tickets="tickets.length" @logout="logout" />

    <main class="container">
      <section class="welcome-card">
        <div>
          <p class="eyebrow">Dashboard</p>
          <h1>IT Support Tickets</h1>
          <p class="welcome-text">
            Create, search, filter, and manage support requests in one place.
          </p>
        </div>

        <button class="logout-mobile" @click="logout">
          Logout
        </button>
      </section>

      <DashboardStats :tickets="tickets" />

      <div class="layout-grid">
        <TicketForm @add-ticket="addTicket" />

        <section class="ticket-panel">
          <SearchBar :search="search" @update-search="search = $event" />

          <StatusFilter
            :status-filter="statusFilter"
            @update-status-filter="statusFilter = $event"
          />

          <TicketList
            :tickets="filteredTickets"
            @update-status="updateStatus"
            @delete-ticket="deleteTicket"
            @edit-ticket="editTicket"
          />
        </section>
      </div>
    </main>
  </template>
</template>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
}

.welcome-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1.5rem;
  padding: 1.75rem;
  background: linear-gradient(145deg, #111827, #0f172a);
  border: 1px solid #263244;
  border-radius: 20px;
  color: #f9fafb;
  box-shadow: 0 16px 35px rgba(0, 0, 0, 0.3);
}

.eyebrow {
  margin: 0 0 0.4rem;
  color: #60a5fa;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.8rem;
}

h1 {
  margin: 0;
  font-size: 2rem;
}

.welcome-text {
  margin: 0.5rem 0 0;
  color: #94a3b8;
}

.layout-grid {
  display: grid;
  grid-template-columns: 380px 1fr;
  gap: 1.5rem;
  align-items: start;
}

.ticket-panel {
  min-width: 0;
}

.logout-mobile {
  background-color: #dc2626;
  color: white;
  border: none;
  padding: 0.85rem 1.2rem;
  cursor: pointer;
  border-radius: 10px;
  font-weight: 800;
}

.logout-mobile:hover {
  background-color: #b91c1c;
}

@media (max-width: 950px) {
  .layout-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 650px) {
  .container {
    padding: 1rem;
  }

  .welcome-card {
    flex-direction: column;
    align-items: flex-start;
  }

  .logout-mobile {
    width: 100%;
  }
}
</style>