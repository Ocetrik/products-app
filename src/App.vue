<template>
  <div class="app">
    <product-list />
  </div>
</template>

<script>
import ProductList from "@/components/ProductList/ProductList.vue";

export default {
  name: "App",
  components: {
    ProductList, 
  },
};
</script>

<style lang="scss">
@import "@/assets/index.css";

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  display: flex;
  justify-content: center;
}
</style>
