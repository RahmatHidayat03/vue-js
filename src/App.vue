<template>
  <div id="app" class="container mt-5">
    <h1>IDShop</h1>
    <product-list v-bind:maximum="maximum" :products="products" @add="item"></product-list>
    <!-- <font-awesome-icon icon="cart-shopping" />
    <price-component :value="4.37"></price-component> -->
  </div>
</template>

<script>
// import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
// import PriceComponent from "./components/PriceComponent.vue";
import ProductList from "./components/ProductList.vue";

export default {
  name: "App",
  data: function () {
    return {
      maximum: 50,
      products: [],
    };
  },

  components: {
    // FontAwesomeIcon,
    // PriceComponent,
    ProductList,
  },
  mounted: function () {
    fetch('https://hplussport.com/api/products/order/price')
      .then((Response) => Response.json())
      .then((data) => {
        this.products = data;
      });
  },
};
</script>
