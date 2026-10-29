# DataTable `v-model:filters` and DatePicker `v-model` lose their type

Reproduction for [primefaces/primevue#8442](https://github.com/primefaces/primevue/issues/8442).

`src/App.vue` binds `DataTable`'s `v-model:filters` to a filter object typed with its own keys, and `DatePicker`'s `v-model` to a `Ref<Date>`. With `strictTemplates: true` and `skipLibCheck: false`, `vue-tsc` rejects both bindings, because each component's emit carries its widest type, `DataTableFilterMeta` and `Date | Date[] | (Date | null)[] | null | undefined`, rather than the bound value's.

```bash
bun install
bun run type-check
```

Expected: no error. Actual: TS2739 on the `DataTable` binding and TS2322 on the `DatePicker` one.
