<template>
  <div class="wrapper">
    <input
      type="text"
      placeholder="Find a Product"
      v-model="productToFind"
      @keypress.enter="findProduct"
      class="input-field"
    />
    <button
      type="button"
      @click="findProduct"
      :class="['btn', resetProducts ? 'reset-button' : 'search-button']"
    >
      {{ resetProducts ? "View All" : "Search" }}
    </button>
  </div>
</template>

<script>
export default {
  name: "FindProduct",
  data() {
    return {
      productToFind: "",
      resetProducts: false,
    };
  },
  methods: {
    findProduct() {
      this.$emit("findProduct", this.productToFind);
      this.resetProducts = true;
      if (this.resetProducts === true && this.productToFind === "") {
        this.resetProducts = false;
      } else {
        this.resetProducts = true;
      }
      this.productToFind = "";
    },
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
  margin-bottom: 8px;
  gap: 8px;
}
.search-button {
  background-color: var(--primary-blue);
}
.reset-button {
  background-color: var(--primary-red);
}
</style>
