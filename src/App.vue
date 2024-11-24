<template>
  <navbar :cart="cart" />
  <div class="contianer">
    <router-view :products="products" :cart="cart" @addToCart="addToCart" />
  </div>
</template>

<script>
import Navbar from "@/components/Navbar";

export default {
  data: function () {
    return {
      cart: [],
      products: [],
    };
  },
  components: {
    Navbar,
  },
  computed: {
    cartTotal() {
      return this.cart.reduce((inc, item) => Number(item.price) + inc, 0);
    },
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
      if (this.cartTotal >= 100) {
        this.salesBtn = "btn-danger";
      }
    },
  },
  created() {
    fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data;
      });
  },
};
</script>

<style lang="scss">
$primary: green;
@import "node_modules/bootstrap/scss/bootstrap";
</style>
