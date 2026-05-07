<script setup>
import Navbar from './components/Navbar.vue'
import TicketForm from './components/TicketForm.vue'
import TicketList from './components/TicketList.vue'
</script>

<template>
  <Navbar />

  <main class="container">
    <TicketForm />

    <TicketList />
  </main>
</template>

<style scoped>
.container {
  padding: 2rem;
  font-family: Arial, sans-serif;
}
</style>