<script setup>
</script>

<template>
  <section class="form-container">
    <h3>Create Ticket</h3>

    <form>
      <input type="text" placeholder="Ticket Title" />

      <textarea placeholder="Describe the issue"></textarea>

      <select>
        <option>Low</option>
        <option>Medium</option>
        <option>High</option>
      </select>

      <button type="submit">
        Submit Ticket
      </button>
    </form>
  </section>
</template>

<style scoped>
.form-container {
  margin-top: 2rem;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

input,
textarea,
select {
  padding: 0.75rem;
}

button {
  background-color: #2563eb;
  color: white;
  border: none;
  padding: 0.75rem;
  cursor: pointer;
}
</style>