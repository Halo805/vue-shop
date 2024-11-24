<template>
  <navbar :cart="cart" :cart-total="cartTotal" :cart-qty="cartQty" />
  <div class="contianer">
    <router-view :products="products" :cart="cart" @addItem="addItem" />
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
      let sum = 0;
      for (let i in this.cart) {
        sum += Number(this.cart[i].product.price) * this.cart[i].qty;
      }
      console.log(sum);
      return sum;
    },
    cartQty: function () {
      let qty = 0;
      for (let i in this.cart) {
        qty += this.cart[i].qty;
      }
      return qty;
    },
  },
  methods: {
    addItem(product) {
      let productIX;
      let existingProduct;
      debugger;
      existingProduct = this.cart.filter(function (item, ix) {
        if (item.product.id == Number(product.id)) {
          productIX = ix;
          return true;
        } else {
          return false;
        }
      });

      if (existingProduct.length) {
        this.cart[productIX].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
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
