<template>
  <div id="app">
    <h3 class="header">Products</h3>
    <div class="card-container">
      <FindProduct @findProduct="filterProducts" />
      <AddProduct />
      <div class="product-container">
        <Product v-for="(product, i) in pagination" :key="i" :product="product">
          <template v-slot:title>{{ product.name }}</template>
        </Product>
      </div>
    </div>
    <FooterSection
      :prodLength="productsLength"
      @sortBy="sortProducts"
      @paginateBy="paginateProducts"
    />
  </div>
</template>

<script>
import Product from "./components/Product.vue";
import AddProduct from "./components/AddProduct.vue";
import FindProduct from "./components/FindProduct.vue";
import FooterSection from "./components/FooterSection.vue";
export default {
  name: "App",
  components: { AddProduct, FindProduct, Product, FooterSection },
  data() {
    return {
      paginateBy: 10,
      filteredProducts: [],
      products: [
        {
          name: "Americano",
          image: "https://picsum.photos/48",
          status: "green",
          date: null,
        },
        {
          name: "Espresso",
          image: "https://picsum.photos/48",
          status: "yellow",
          date: null,
        },
        {
          name: "Mocha",
          image: "",
          status: "green",
          date: null,
        },
        {
          name: "White Mocha",
          image: "",
          status: "yellow",
          date: 704305433,
        },
        {
          name: "Latte",
          image: "https://picsum.photos/48",
          status: "green",
          date: 1666715033,
        },
        {
          name: "Cappucino",
          image: "https://picsum.photos/48",
          status: "green",
          date: null,
        },
        {
          name: "Walking with Giants",
          image: "https://picsum.photos/48",
          status: "green",
          date: null,
        },
        {
          name: "Turbinator 2",
          image: "https://picsum.photos/48",
          status: "red",
          date: null,
        },
        {
          name: "Super Cali Fragilistic Expialidocious",
          image: "",
          status: "red",
          date: 704305433,
        },
        {
          name: "Baseball Hat",
          image: "https://picsum.photos/48",
          status: "green",
          date: null,
        },
        {
          name: "Americano",
          image: "https://picsum.photos/48",
          status: "green",
          date: null,
        },
        {
          name: "Espresso",
          image: "https://picsum.photos/48",
          status: "yellow",
          date: null,
        },
        {
          name: "Mocha",
          image: "",
          status: "green",
          date: null,
        },
        {
          name: "White Mocha",
          image: "",
          status: "yellow",
          date: 704305433,
        },
        {
          name: "Latte",
          image: "https://picsum.photos/48",
          status: "green",
          date: 1666715033,
        },
        {
          name: "Cappucino",
          image: "https://picsum.photos/48",
          status: "green",
          date: null,
        },
        {
          name: "Walking with Giants",
          image: "https://picsum.photos/48",
          status: "green",
          date: null,
        },
        {
          name: "Turbinator 2",
          image: "https://picsum.photos/48",
          status: "red",
          date: null,
        },
        {
          name: "Super Cali Fragilistic Expialidocious",
          image: "",
          status: "red",
          date: 704305433,
        },
        {
          name: "Baseball Hat",
          image: "https://picsum.photos/48",
          status: "green",
          date: null,
        },
      ],
    };
  },
  computed: {
    pagination() {
      return this.filteredProducts.length
        ? this.filteredProducts.slice(0, this.paginateBy)
        : this.products.slice(0, this.paginateBy);
    },
    productsLength() {
      return this.products.length;
    },
  },
  methods: {
    sortProducts(sortOption) {
      this.filteredProducts = this.products;
      if (sortOption === "status") {
        this.filteredProducts.sort(function (a, b) {
          if (a.status < b.status) {
            return -1;
          }
          if (a.status > b.status) {
            return 1;
          }
          return 0;
        });
      } else {
        this.filteredProducts.sort(function (a, b) {
          if (a.name < b.name) {
            return -1;
          }
          if (a.name > b.name) {
            return 1;
          }
          return 0;
        });
      }
    },
    paginateProducts(newAmount) {
      this.paginateBy = newAmount;
    },
    filterProducts(searchTerm) {
      this.filteredProducts = this.products;
      this.filteredProducts = this.products.filter((product) =>
        product.name.toLowerCase().includes(searchTerm.toLowerCase())
      );
    },
  },
};
</script>

<style>
#app {
  background-color: #ececec;
  padding: 20px 16px;
  margin: 0 auto;
  max-width: 1100px;
  min-height: 100vh;
}
@media screen and (min-width: 728px) {
  .product-container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-column-gap: 30px;
    grid-row-gap: 0px;
  }
}
.card-container {
  margin-top: 16px;
  background: #fff;
  padding: 16px;
}
</style>
