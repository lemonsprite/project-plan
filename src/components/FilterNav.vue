<template>
  <div class="filter-nav">
    <button
      @click="updateFilter('all')"
      :class="{ active: filterInit === 'all' }"
    >
      Lihat Semua
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: filterInit === 'completed' }"
    >
      Selesai
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: filterInit === 'ongoing' }"
    >
      Ongoing
    </button>
  </div>
</template>

<script>
export default {
  props: ["filterInit"],
  methods: {
    updateFilter(params) {
      this.$emit("filter", params);
    },
  },
};
</script>
<style>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
  color: #555;
}
</style>
