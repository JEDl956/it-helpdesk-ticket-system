<script setup>
defineProps({
  totalTickets: {
    type: Number,
    default: 0,
  },
})
</script>

<template>
  <nav class="navbar">
    <div class="left">
      <div class="logo">🖥️</div>

      <div>
        <h2>IT Help Desk</h2>
        <p>Ticket Management Dashboard</p>
      </div>
    </div>

    <div class="right">
      <div class="ticket-counter">
        <span class="count">{{ totalTickets }}</span>
        <span class="label">Tickets</span>
      </div>

      <button class="logout-btn">
        Logout
      </button>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  padding: 1.2rem 2rem;
  background: linear-gradient(145deg, #020617, #0f172a);
  border-bottom: 1px solid #1e293b;
  color: white;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.35);
}

.left {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.logo {
  width: 56px;
  height: 56px;
  display: grid;
  place-items: center;
  background-color: #111827;
  border: 1px solid #334155;
  border-radius: 16px;
  font-size: 1.6rem;
}

h2 {
  margin: 0;
  font-size: 1.5rem;
}

p {
  margin: 0.25rem 0 0;
  color: #94a3b8;
  font-size: 0.9rem;
}

.right {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.ticket-counter {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0.7rem 1rem;
  background-color: #111827;
  border: 1px solid #334155;
  border-radius: 12px;
}

.count {
  font-size: 1.2rem;
  font-weight: 800;
  color: #60a5fa;
}

.label {
  font-size: 0.75rem;
  color: #94a3b8;
}

.logout-btn {
  border: none;
  background-color: #dc2626;
  color: white;
  padding: 0.8rem 1.2rem;
  border-radius: 10px;
  cursor: pointer;
  font-weight: 700;
}

.logout-btn:hover {
  background-color: #b91c1c;
}

@media (max-width: 700px) {
  .navbar {
    flex-direction: column;
    align-items: flex-start;
  }

  .right {
    width: 100%;
    justify-content: space-between;
  }

  .logout-btn {
    width: 100%;
  }
}
</style>