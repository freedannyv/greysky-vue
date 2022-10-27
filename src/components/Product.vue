<template>
  <div>
    <div
      @click="displayProductDetails = !displayProductDetails"
      class="product-container"
    >
      <div class="product-info">
        <div class="image-container">
          <img v-if="product.image" :src="fetchImage" :alt="product.name" />
        </div>
        <div :class="['status', statusColor]" />
        <slot name="title"></slot>
      </div>
      <div class="date-info">
        <span>{{ formatDate }}</span>
        <svg
          width="10"
          height="6"
          viewBox="0 0 10 6"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          :class="['chevron', { 'chevron-rotate': displayProductDetails }]"
        >
          <path
            d="M9.47136 0.471344C9.34634 0.346364 9.1768 0.276154 9.00003 0.276154C8.82325 0.276154 8.65371 0.346364 8.52869 0.471344L5.47136 3.52868C5.34461 3.65034 5.17572 3.71827 5.00003 3.71827C4.82434 3.71827 4.65545 3.65034 4.52869 3.52868L1.47136 0.471344C1.34563 0.349906 1.17722 0.282709 1.00243 0.284228C0.827629 0.285747 0.660421 0.35586 0.536815 0.479465C0.41321 0.603071 0.343097 0.770279 0.341578 0.945077C0.340059 1.11987 0.407256 1.28828 0.528694 1.41401L3.58536 4.47134C3.77108 4.6571 3.99158 4.80445 4.23425 4.90498C4.47692 5.00551 4.73702 5.05725 4.99969 5.05725C5.26237 5.05725 5.52247 5.00551 5.76514 4.90498C6.00781 4.80445 6.22831 4.6571 6.41403 4.47134L9.47136 1.41401C9.59634 1.28899 9.66655 1.11945 9.66655 0.942677C9.66655 0.765901 9.59634 0.596363 9.47136 0.471344Z"
            fill="#626466"
          />
        </svg>
      </div>
    </div>
    <Transition name="fade">
      <ProductExtra v-show="displayProductDetails" :product="product">
        <template v-slot:image>
          <div v-if="product.image" class="image-container">
            <img :src="product.image" :alt="product.name" class="card-image" />
          </div>
        </template>
        <template v-slot:title>
          <p class="title-decoration">{{ product.name }}</p>
        </template>
        <template v-slot:description>
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus
            cumque, vel illum ad distinctio debitis excepturi a maiores harum
            minima ratione dignissimos vitae ut consequuntur qui labore
            recusandae. Sed, mollitia, incidunt reiciendis fuga voluptatum
            accusamus sit dignissimos aliquid sint culpa ad quis ea vero quae
            impedit consequatur laboriosam dolorum totam?
          </p>
        </template>
      </ProductExtra>
    </Transition>
  </div>
</template>

<script>
import ProductExtra from "./ProductExtra.vue";

export default {
  name: "Product",
  props: ["product"],
  components: { ProductExtra },
  data() {
    return {
      displayProductDetails: false,
    };
  },
  computed: {
    fetchImage() {
      return this.product?.image;
    },
    statusColor() {
      switch (this.product.status) {
        case "green":
          return "status-green";
        case "yellow":
          return "status-yellow";
        case "red":
          return "status-red";
        default:
          return "status-red";
      }
    },
    formatDate() {
      if (this.product?.date != null) {
        const date = new Date(this.product.date * 1000);
        console.log(date);
        return `${date.getDate()}/${date.getMonth()}/${date.getFullYear()}`;
      } else {
        return "";
      }
    },
  },
};
</script>

<style scoped>
.product-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 48px;
  border-bottom: 1px solid var(--grey-light);
  padding: 0 8px;
  cursor: pointer;
}
.product-container:hover {
  background-color: var(--grey-light);
}

.product-info {
  display: flex;
  align-items: center;
  gap: 11px;
}

.image-container {
  height: 24px;
  width: 24px;
}

img {
  width: 100%;
}
.status {
  height: 9px;
  width: 9px;
  border-radius: 50%;
}

.status-green {
  background: var(--status-green);
}
.status-yellow {
  background: var(--status-yellow);
}
.status-red {
  background: var(--status-red);
}
.date-info {
  display: flex;
  align-items: center;
  gap: 20px;
}
.chevron {
  transition: transform 0.4s ease-in-out;
}
.chevron-rotate {
  transform: rotate(180deg);
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
