<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        v-for="filter in filters"
        :key="filter"
        :class="{'button--primary' : activeFilter === filter}"
        class="button"
        @click="setFilter(filter)"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>
<script lang="ts">
import {defineComponent, PropType} from 'vue'
import {Filters} from "@/types/Filters";

export default defineComponent({
  name: "AppFilters",
  props: {
    activeFilter: {
      type: String as PropType<Filters>,
      required: true
    }
  },
  emits: {
    'set-filter': (filter: Filters) => filter,
  },
  data() {
    return {
      filters: ['All', 'Active', 'Done']
    }
  },
  methods: {
    setFilter(filter: Filters) {
      this.$emit('set-filter', filter)
    }
  }
})
</script>
<style scoped>

</style>
