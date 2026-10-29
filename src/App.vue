<script setup lang="ts">
import { ref } from 'vue';
import DataTable, { type DataTableFilterMetaData } from 'primevue/datatable';
import Column from 'primevue/column';
import DatePicker from 'primevue/datepicker';

interface Person {
  id: number;
  name: string;
}

const people = ref<Person[]>([
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
]);

const filters = ref<{ global: DataTableFilterMetaData; name: DataTableFilterMetaData }>({
  global: { value: null, matchMode: 'contains' },
  name: { value: null, matchMode: 'startsWith' },
});

const day = ref<Date>(new Date(2026, 0, 1));
</script>

<template>
  <div style="max-width: 600px; margin: 40px auto; font-family: system-ui, sans-serif">
    <h2>v-model loses its type through DefineComponent</h2>

    <DataTable v-model:filters="filters" :value="people" filter-display="row">
      <Column field="name" header="Name" />
    </DataTable>

    <DatePicker v-model="day" />

    <p>Run <code>bun run type-check</code> in the terminal.</p>
  </div>
</template>
