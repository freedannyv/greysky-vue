<template>
  <div class="wrapper">
    <input type="text" placeholder="Product Name" class="input-field" />
    <button type="button" class="btn search-button">Add Product</button>
  </div>
</template>

<script>
export default {
  name: "AddProduct",
};
</script>

<style scoped>
.wrapper {
  display: flex;
  margin-bottom: 8px;
  gap: 8px;
}
.search-button {
  background-color: var(--primary-green);
}
</style>
