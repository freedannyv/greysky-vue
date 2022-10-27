<template>
  <div>
    <slot name="image"></slot>
    <slot name="title"></slot>
    <slot name="description"></slot>
  </div>
</template>

<script>
export default {
  name: "ProductExtra",
};
</script>

<style scoped>
.card-image {
  object-fit: cover;
  object-position: center;
  width: 100%;
  height: 100%;
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;
}
.title-decoration {
  padding: 10px 0;
  border-bottom: 1px solid var(--grey-light);
  margin-bottom: 10px;
}
</style>
