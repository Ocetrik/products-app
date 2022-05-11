<template>
  <div class="product">
    <div class="product__img">
      <img :src="product.img" alt="" />
    </div>
    <div class="product__info">
      <div class="info__title">{{ product.title }}</div>
      <div class="info__body">{{ product.body }}</div>
      <div class="info__price">{{ product.price }} руб.</div>
    </div>
    <button @click="deleteProduct" class="product__basket">
      <img src="@/static/basket.png" alt="" />
    </button>
  </div>
</template>

<script>
export default {
  name: "Product",
  data: () => ({}),
  props: {
    product: {
      type: Object,
      default: {},
    },
  },
  methods: {
    deleteProduct() {
      this.$emit("delete", this.product);
    },
  },
};
</script>

<style lang="scss" scoped>
.product {
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  max-width: 332px;
  position: relative;

  &__basket {
    position: absolute;
    right: -8px;
    top: -8px;
    background: #ff8484;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    border: #ffffff;
    padding: 8px;
    display: none;
    cursor: pointer;
  }

  &__info {
    padding: 16px;
  }
}

.info {
  &__title {
    font-family: "SourceSansPro-Semibold";
    font-size: 20px;
    line-height: 25px;
    color: #3f3f3f;
  }

  &__body {
    padding-top: 16px;
    font-family: "SourceSansPro-Regular";
    font-size: 16px;
    line-height: 20px;
    color: #3f3f3f;
  }

  &__price {
    padding-top: 32px;
    font-family: "SourceSansPro-Semibold";
    font-size: 24px;
    line-height: 30px;
    color: #3f3f3f;
  }
}

.product:hover .product__basket {
  display: block;
}

img {
  width: 100%;
}
</style>