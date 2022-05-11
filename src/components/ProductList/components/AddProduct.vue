<template>
  <div class="add-product">
    <div class="add-product__name">
      <div class="name__title">
        <div class="title__text">Наименование товара</div>
        <div class="title__required-name-img">
          <img src="@/static/required.svg" alt="" />
        </div>
      </div>
      <input
        :class="{ error: isTitleEmpty }"
        v-model="product.title"
        placeholder="Введите наименование товара"
        type="text"
        @click="showTitleErrorMsg"
      />
      <div v-if="isTitleEmpty" class="error-msg">
        Поле является обязательным
      </div>
    </div>
    <div class="add-product__description">
      <div class="description__title title">
        <div class="title__text">Описание товара</div>
      </div>
      <textarea
        v-model="product.body"
        placeholder="Введите описание товара"
      ></textarea>
    </div>
    <div class="add-product__url">
      <div class="url__title title">
        <div class="title__text">Ссылка на изображение товара</div>
        <div class="title__required-url-img">
          <img src="@/static/required.svg" alt="" />
        </div>
      </div>
      <input
        :class="{ error: isImgEmpty }"
        v-model="product.img"
        placeholder="Введите ссылку"
        type="text"
        @click="showImgErrorMsg"
      />
      <div v-if="isImgEmpty" class="error-msg">Поле является обязательным</div>
    </div>
    <div class="add-product__price">
      <div class="price__title title">
        <div class="title__text">Цена товара</div>
        <div class="title__required-price-img">
          <img src="@/static/required.svg" alt="" />
        </div>
      </div>
      <input
        :class="{ error: isPriceEmpty }"
        v-model="product.price"
        placeholder="Введите цену"
        type="number"
        @click="showPriceErrorMsg"
      />
      <div v-if="isPriceEmpty" class="error-msg">
        Поле является обязательным
      </div>
    </div>
    <button
      :disabled="isEnableBtn"
      :class="{ active: !isEnableBtn }"
      class="add-product__btn"
      @click="addProduct"
    >
      Добавить товар
    </button>
  </div>
</template>

<script>
export default {
  name: "AddProduct",
  data: () => ({
    isTitleEmpty: false,
    isImgEmpty: false,
    isPriceEmpty: false,
    product: {
      title: "",
      body: "",
      img: "",
      price: "",
    },
  }),

  methods: {
    addProduct() {
      this.$emit("add", { ...this.product, id: Date.now() });
      this.product = {
        title: "",
        body: "",
        img: "",
        price: "",
      };
    },
    showTitleErrorMsg() {
      if (this.product.title === "") {
        this.isTitleEmpty = true;
      } else {
        this.isTitleEmpty = false;
      }
    },
    showImgErrorMsg() {
      if (this.product.img === "") {
        this.isImgEmpty = true;
      } else {
        this.isImgEmpty = false;
      }
    },
    showPriceErrorMsg() {
      if (this.product.price === "") {
        this.isPriceEmpty = true;
      } else {
        this.isPriceEmpty = false;
      }
    },
  },
  computed: {
    isEnableBtn() {
      return (
        this.product.title === "" ||
        this.product.img === "" ||
        this.product.price === ""
      );
    },
  },
  watch: {
    product: {
      handler() {
        this.showTitleErrorMsg();
        this.showImgErrorMsg();
        this.showPriceErrorMsg();
      },
      deep: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.add-product {
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  max-width: 332px;
  padding: 24px;
  position: sticky;
  top: 24px;
}

.title {
  margin-top: 16px;

  &__text {
    font-family: "SourceSansPro-Regular";
    font-size: 10px;
    line-height: 13px;
    color: #49485e;
  }

  &__required-name-img {
    position: absolute;
    bottom: 5px;
    left: 99px;
  }

  &__required-url-img {
    position: absolute;
    bottom: 5px;
    left: 139px;
  }

  &__required-price-img {
    position: absolute;
    bottom: 5px;
    left: 55px;
  }
}

input {
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: #ffffff;
  margin-top: 4px;
  min-width: 284px;
  padding-top: 10px;
  padding-bottom: 11px;
  padding-left: 16px;
  font-family: "SourceSansPro-Regular";
  font-size: 12px;
  line-height: 15px;
  transition: all 0.5s ease 0s;

  &:focus {
    transition: all 0.5s ease 0s;
    box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.3);
  }
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

textarea {
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border: #ffffff;
  border-radius: 4px;
  min-width: 284px;
  min-height: 108px;
  padding-top: 10px;
  padding-left: 16px;
  font-family: "SourceSansPro-Regular";
  font-size: 12px;
  line-height: 15px;
  transition: all 0.5s ease 0s;
  resize: none;

  &:focus {
    transition: all 0.5s ease 0s;
    box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.3);
  }
}

.error {
  border: 1px solid #ff8484;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  &-msg {
    color: #ff8484;
    font-family: "SourceSansPro-Regular";
    font-size: 8px;
    line-height: 10px;
  }
}

.description__title {
  position: relative;
  display: flex;
}

.name__title {
  display: flex;
  position: relative;
}

.url__title {
  position: relative;
  display: flex;
}

.price__title {
  position: relative;
  display: flex;
}

.add-product__btn {
  border-radius: 10px;
  background: #eeeeee;
  border: 0;
  padding: 10px 95px 11px 96px;
  margin-top: 34px;
  font-family: "Inter-Semibold";
  color: #b4b4b4;
  font-size: 12px;
  line-height: 15px;
}

.active {
  background: #7bae73;
  color: #ffffff;
  transition: all 0.5s ease 0s;
  cursor: pointer;

  &:hover {
    transition: all 0.5s ease 0s;
    box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.3);
  }
}
</style>