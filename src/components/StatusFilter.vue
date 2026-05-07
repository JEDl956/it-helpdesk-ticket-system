<script setup>
defineProps({
  statusFilter: {
    type: String,
    required: true,
  },
})

defineEmits(['update-status-filter'])
</script>

<template>
  <section class="filter">
    <select
      :value="statusFilter"
      @change="$emit('update-status-filter', $event.target.value)"
    >
      <option>All</option>
      <option>Open</option>
      <option>In Progress</option>
      <option>Closed</option>
    </select>
  </section>
</template>

<style scoped>
.filter {
  margin-bottom: 1.5rem;
}

select {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ccc;
  border-radius: 6px;
}
</style>