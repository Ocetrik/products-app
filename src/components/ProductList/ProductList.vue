<template>
  <div class="product-list">
    <div class="product-list__header">
      <div class="header__title">Добавление товара</div>
      <div class="header__sort-product">
        <sort-product v-model="selectedSort" :options="sortOptions" />
      </div>
    </div>
    <div class="product-list__wrapper">
      <div class="product-list__add-product">
        <add-product @add="addProduct" />
      </div>
      <div class="product-list__product">
        <transition-group name="product-item">
          <product-item
            v-for="i in sortedProducts"
            :key="i.id"
            @delete="deleteProduct"
            :product="i"
          />
        </transition-group>
      </div>
    </div>
  </div>
</template>

<script>
import { STATIC_PRODUCT } from "@/data/STATIC_PRODUCT.js";
import ProductItem from "@/components/ProductList/components/ProductItem.vue";
import AddProduct from "@/components/ProductList/components/AddProduct.vue";
import SortProduct from "@/components/ProductList/components/SortProduct.vue";

export default {
  name: "ProductList",
  components: {
    ProductItem,
    AddProduct,
    SortProduct,
    STATIC_PRODUCT,
  },
  data: () => ({
    products: STATIC_PRODUCT,
    selectedSort: "",
    sortOptions: [
      { value: "title", name: "По названию" },
      { value: "price", name: "По цене min" },
      { value: "price", name: "По цене max" },
    ],
  }),
  methods: {
    deleteProduct(product) {
      this.products = this.products.filter((item) => item.id !== product.id);
    },
    addProduct(product) {
      this.products.push(product);
    },
  },
  computed: {
    sortedProducts() {
      return [...this.products].sort((post1, post2) => {
        return post1[this.selectedSort]?.localeCompare(
          post2[this.selectedSort]
        );
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.product-list {
  padding: 32px;
  position: relative;
}

.header__title {
  font-family: "SourceSansPro-Semibold";
  font-size: 28px;
  line-height: 35px;
  color: #3f3f3f;
}

.product-list__wrapper {
  display: flex;
  gap: 16px;
  margin-top: 16px;
}

.product-list__product {
  display: grid;
  gap: 16px;
  grid-template-columns: 1fr 1fr 1fr;
}

.product-list__header {
  display: flex;
  justify-content: space-between;
}

.product-item-item {
  display: inline-block;
  margin-right: 10px;
}

.product-item-enter-active,
.product-item-leave-active {
  transition: all 1s ease;
}

.product-item-enter-from,
.product-item-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>