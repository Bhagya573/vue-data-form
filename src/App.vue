<template>
  <div id="app" class="container">
    <FormComponent @add-item="addItem" />
    <TableComponent :data="tableData" />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import FormComponent from './components/FormComponent.vue';
import TableComponent from './components/TableComponent.vue';

export default {
  name: 'App',
  components: {
    FormComponent,
    TableComponent,
  },
  setup() {
    // Create a reactive reference for tableData
    const tableData = ref([]);

    // Load data from localStorage
    const loadDataFromStorage = () => {
      const storedData = localStorage.getItem('tableData');
      if (storedData) {
        tableData.value = JSON.parse(storedData);
      }
    };

    // Add a new item to the table and save to localStorage
    const addItem = (newItem) => {
      tableData.value.push(newItem);
      saveDataToStorage();
    };

    // Save table data to localStorage
    const saveDataToStorage = () => {
      localStorage.setItem('tableData', JSON.stringify(tableData.value));
    };

    // Run loadDataFromStorage when the component is mounted
    onMounted(() => {
      loadDataFromStorage();
    });

    // Return reactive data and methods to the template
    return {
      tableData,   
      addItem,  
    };
  },
};
</script>
