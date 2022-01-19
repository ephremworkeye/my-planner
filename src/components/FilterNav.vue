<template>
  <nav class="filter-nav">
      <button @click="updateFilter('all')" 
        :class="{ active: current=== 'all' }">
          View All
      </button>
      <button @click="updateFilter('completed')" 
        :class="{ active: current === 'completed'}">
          Completed
      </button>
      <button @click="updateFilter('ongoing')" 
      :class="{ active: current === 'ongoing' }">
          Ongoing
      </button>
  </nav>
</template>

<script>
export default {
    props: ['current'],
    methods: {
        updateFilter(by) {
            this.$emit('filterChange', by)
        }
    },

}
</script>

<style>
.filter-nav button {
  background: none;
  border: 1px solid green;
  margin: 10px 15px 10px 0;
  padding: 10px 20px;
  font-size: 1.1rem;
  text-transform: uppercase;
  cursor: pointer;
  font-weight: bold;
  border-radius: 10px;
  color: rgb(82, 80, 80);

}
.filter-nav button.active {
    background: green;
    color: white
}
</style>