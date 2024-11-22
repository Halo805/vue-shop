<template>
  {{ dollar(amount) }}
</template>

<script>
export default {
  name: "Currency",
  props: ["amount"],
  methods: {
    dollar(value) {
      return "$" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>
