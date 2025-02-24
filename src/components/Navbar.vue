<template>
  <nav class="navbar navbar-light sticky-top mr-3">
    <div
      v-if="cart.length"
      class="w-100 navbar-text ml-auto d-flex justify-content-end position-relative cart-dropdown"
    >
      <div
        class="mr-auto d-flex align-items-end flex-column bd-highlight mb-3 position-absolute"
      >
        <div class="mb-2">
          <span class="font-weight-bold bg-white">
            <currency :amount="cartTotal"></currency>
          </span>
          <button
            @click="toggleCartMenu"
            class="btn btn-sm btn-success ml-3"
            id="cartDropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >
            <fa icon="shopping-cart" />{{ cartQty }}
          </button>
        </div>
        <cart-dropdown
          :cart="cart"
          :displayCart="displayCart"
          @toggle-cart-menu="toggleCartMenu"
        />
      </div>
    </div>
  </nav>
</template>

<script>
import Currency from "@/components/Currency";
import CartDropdown from "@/components/CartDropdown.vue";

export default {
  name: "Navbar",
  data: function () {
    return {
      displayCart: false,
    };
  },
  components: {
    Currency,
    CartDropdown,
  },
  methods: {
    toggleCartMenu() {
      this.displayCart = !this.displayCart;
    },
  },
  props: ["cart", "cartTotal", "cartQty"],
};
</script>

<style>
.cart-dropdown {
  margin-right: 20px;
}
</style>
