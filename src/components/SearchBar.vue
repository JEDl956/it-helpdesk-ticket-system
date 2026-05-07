<script setup>
defineProps({
  search: {
    type: String,
    required: true,
  },
})

defineEmits(['update-search'])
</script>

<template>
  <section class="search-card">
    <div class="search-icon">🔎</div>

    <input
      :value="search"
      type="text"
      placeholder="Search tickets by title, description, or priority..."
      @input="$emit('update-search', $event.target.value)"
    />
  </section>
</template>

<style scoped>
.search-card {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  margin: 1.5rem 0;
  padding: 0.85rem 1rem;
  background: linear-gradient(145deg, #111827, #0f172a);
  border: 1px solid #263244;
  border-radius: 16px;
  box-shadow: 0 12px 28px rgba(0, 0, 0, 0.25);
}

.search-icon {
  color: #94a3b8;
  font-size: 1.2rem;
}

input {
  width: 100%;
  padding: 0.75rem;
  background-color: transparent;
  color: #f9fafb;
  border: none;
  outline: none;
  font-size: 1rem;
}

input::placeholder {
  color: #94a3b8;
}
</style>