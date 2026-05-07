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
    const matchesSearch = ticket.title
      .toLowerCase()
      .includes(search.value.toLowerCase())

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
  const ticket = tickets.value.find(
    (ticket) => ticket.id === updatedTicket.id,
  )

  if (ticket) {
    ticket.title = updatedTicket.title
    ticket.description = updatedTicket.description
  }
}
</script>

<template>
  <template v-if="!isLoggedIn">
    <LoginForm @login="login" />
  </template>

  <template v-else>
    <Navbar />

    <main class="container">
      <div class="top-bar">
        <button class="logout" @click="logout">
          Logout
        </button>
      </div>

      <DashboardStats :tickets="tickets" />

      <TicketForm @add-ticket="addTicket" />

      <SearchBar
        :search="search"
        @update-search="search = $event"
      />

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
    </main>
  </template>
</template>

<style scoped>
.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
}

.top-bar {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 1rem;
}

.logout {
  background-color: #dc2626;
  color: white;
  border: none;
  padding: 0.75rem 1rem;
  cursor: pointer;
  border-radius: 8px;
  font-weight: bold;
}

.logout:hover {
  background-color: #b91c1c;
}
</style>