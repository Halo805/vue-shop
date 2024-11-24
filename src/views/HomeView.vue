<template>
  <section class="container">
    <range-selector :products="filteredProducts" v-model="max" />
    <product-list :products="filteredProducts" />
  </section>
</template>

<script>
import ProductList from "@/components/ProductList";
import RangeSelector from "@/components/RangeSelector";

/* @ is an alias to /src */

export default {
  name: "HomeView",
  data: function () {
    return {
      max: 50,
      cart: [],
    };
  },
  components: {
    RangeSelector,
    ProductList,
  },
  computed: {
    filteredProducts() {
      return this.products.filter(item => item.price < Number(this.max));
    },
  },
  props: ["products"],
};
</script>
