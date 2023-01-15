<template>
  <nav class="text-gray-400 py-4 flex gap-4">
    <button
      :class="{ 'text-gray-800': current === 'all' }"
      @click="updateFilter('all')"
    >
      View All
    </button>
    <button
      :class="{ 'text-gray-800': current === 'completed' }"
      @click="updateFilter('completed')"
    >
      Completed
    </button>
    <button
      :class="{ 'text-gray-800': current === 'ongoing' }"
      @click="updateFilter('ongoing')"
    >
      Ongoing
    </button>
  </nav>
</template>
<script>
export default {
  name: 'FilterNav',
  props: ['current'],
  methods: {
    updateFilter(by) {
      this.$emit('updateFilter', by);
    },
  },
};
</script>
