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
  <section class="search">
    <input
      :value="search"
      @input="$emit('update-search', $event.target.value)"
      type="text"
      placeholder="Search tickets..."
    />
  </section>
</template>

<style scoped>
.search {
  margin: 1.5rem 0;
}

input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ccc;
  border-radius: 6px;
}
</style>