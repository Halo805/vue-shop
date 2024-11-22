<template>
  <navbar :cart="cart" />
  <div class="contianer">
    <router-view :cart="cart" @addToCart="addToCart" />
  </div>
</template>

<script>
import Navbar from "@/components/Navbar";

export default {
  data: function () {
    return {
      cart: [],
      displayCart: false,
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
};
</script>

<style lang="scss">
$primary: green;
@import "node_modules/bootstrap/scss/bootstrap";

.products-enter-active,
.products-leave-active {
  transition: all 0.5s ease-in-out;
}

.products-enter-from {
  opacity: 0;
  transform: translateX(300px);
}

.products-leave-to {
  opacity: 0;
  transform: translateX(-300px);
}
</style>
