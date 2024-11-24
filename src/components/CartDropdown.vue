<template>
  <div class="dropdown-clip" v-if="cart.length > 0">
    <transition name="dropdown">
      <div
        v-if="displayCart"
        class="list-group bg-white"
        aria-labelledby="cartDropdown"
      >
        <div v-for="(item, index) in cart" :key="index">
          <div class="dropdown-item-text text-nowrap text-right align-middle">
            <span class="badge bg-success align-text-top mr-2">
              {{ item.qty }}
            </span>
            {{ item.product.name }}
            <b>
              <currency :amount="item.qty * Number(item.product.price)" />
            </b>
            <button
              @click.stop="this.$parent.$emit('deleteItem', index)"
              class="btn btn-sm btn-danger mr-2 ml-2"
            >
              -
            </button>
          </div>
        </div>
        <router-link
          to="/checkout"
          class="btn btn-sm btn-success text-thite float-right mr-2 mt-2"
        >
          View Checkout
        </router-link>
      </div>
    </transition>
  </div>
</template>
<script>
import Currency from "@/components/Currency";
export default {
  components: {
    Currency,
  },
  emits: ["deleteItem"],
  props: ["cart", "displayCart"],
};
</script>

<style>
.dropdown-clip {
  overflow: hidden;
}
.dropdown-enter-actice,
.dropdown-leave-active {
  transition: all 0.5s ease-in-out;
  transform: auto;
}
.dropdown-enter-from,
.dropdown-enter-to {
  opacity: 0;
  transform: translateY(-300px);
}
</style>
