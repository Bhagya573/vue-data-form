<template>
  <div class="table-container">
    <h3>Data Table</h3>
    <div class="table-grid">
      <!-- Table Headers -->
      <div class="table-header">Name</div>
      <div class="table-header">Age</div>

      <!-- Table Data Rows -->
      <div v-for="(item, index) in data" :key="index" class="table-row">
        <div class="table-cell">{{ item.name }}</div>
        <div class="table-cell">{{ item.age }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TableComponent',
  props: {
    data: {
      type: Array,
      required: true,
    },
  },
});
</script>