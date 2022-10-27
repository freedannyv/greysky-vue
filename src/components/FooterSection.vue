<template>
  <div class="section-wrapper">
    <div>
      Page <span>1</span> of <span>{{ totalPages }}</span>
    </div>
    <div class="sort-by-wrapper">
      Sort by
      <span>
        <select name="sortBy" @change="updateSort($event)">
          <option value="name">Order</option>
          <option value="status">Status</option>
        </select>
      </span>
    </div>
    <select
      @change="updatePagination"
      name="paginate"
      v-model="paginationValue"
    >
      <option value="10">10</option>
      <option value="20">20</option>
      <option value="50">50</option>
      <option value="100">100</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "FooterSection",
  inject: ["productsLength"],
  data() {
    return {
      paginationValue: 10,
    };
  },
  computed: {
    totalPages() {
      let totalPages = Math.ceil(this.productsLength / this.paginationValue);
      return totalPages;
    },
  },
  methods: {
    updateSort(e) {
      this.$emit("sortBy", e.target.value);
    },
    updatePagination() {
      this.$emit("paginateBy", this.paginationValue);
    },
  },
};
</script>

<style scoped>
.section-wrapper {
  display: flex;
  justify-content: space-between;
  font-size: 12px;
  gap: 4px;
}
div {
  padding: 8px 16px;
}
span {
  font-weight: 700;
}
.sort-by-wrapper {
  display: flex;
}
</style>
